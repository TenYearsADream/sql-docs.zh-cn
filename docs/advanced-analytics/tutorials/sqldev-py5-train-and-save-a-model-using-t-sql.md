---
title: 训练和保存使用 T-SQL 的 SQL Server 机器学习的 Python 模型
description: Python 教程显示如何训练和保存使用 TRANSACT-SQL 在 SQL Server 上的模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2e0505cf847a091a5650b392aab56f486cee16aa
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511244"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>训练和保存使用 T-SQL 的 Python 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是教程的一部分[SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步骤中，了解如何使用 Python 包对机器学习模型定型**scikit-了解**并**revoscalepy**。 这些 Python 库已随 SQL Server 机器学习服务。

在加载模块，并调用要创建并定型模型时使用的 SQL Server 存储过程的必要函数。 该模型所需在前面的课程中设计的数据功能。 最后，保存已训练的模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>将示例数据拆分为定型集和测试集

1. 创建名为存储的过程**PyTrainTestSplit** nyctaxi_sample 表中的数据划分为两个部分： nyctaxi_sample_training 和 nyctaxi_sample_testing。 

    此存储的过程应已创建，但你可以运行下面的代码来创建它：

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. 若要将使用自定义拆分数据，运行存储的过程，并键入一个整数来表示百分比的数据分配到训练集。 例如，以下语句会分配到训练集的数据的 60%。

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>生成逻辑回归模型

已准备好数据后，可用于训练模型。 执行此操作通过调用存储过程运行某些 Python 代码中，将作为输入定型数据的表。 对于本教程中，您将创建两个模型，这两种二进制分类模型：

+ 存储的过程**PyTrainScikit**创建一个提示预测模型使用**scikit-了解**包。
+ 存储的过程**TrainTipPredictionModelRxPy**创建一个提示预测模型使用**revoscalepy**包。

每个存储的过程使用的输入的数据提供要创建并定型逻辑回归模型。 所有 Python 代码都包装在系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

若要更加轻松地重新训练模型对新数据，您对 sp_execute_exernal_script 的调用包装在另一个存储过程中，并在新的定型数据作为参数传递。 本部分将引导你完成该过程。

### <a name="pytrainscikit"></a>PyTrainScikit

1.  在中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，打开一个新**查询**窗口，并运行以下语句以创建存储的过程**PyTrainScikit**。  存储的过程包含输入数据的定义，因此无需提供输入的查询。

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from sklearn.linear_model import LogisticRegression
    
    ##Create SciKit-Learn logistic regression model
    X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
    y = numpy.ravel(InputDataSet[["tipped"]])
    
    SKLalgo = LogisticRegression()
    logitObj = SKLalgo.fit(X, y)
    
    ##Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

2. 运行以下 SQL 语句插入到训练的模型表 nyc\_taxi_models。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    数据处理和模型调整可能需要几分钟。 将其通过管道传递到 Python 的消息**stdout**流显示在**消息**窗口中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 例如：

    *来自外部脚本的 STDOUT 消息：*
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 打开表*nyc\_taxi_models*。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

此存储的过程使用的新**revoscalepy**包，这是新 Python 包。 它包含的对象、 转换和类似于针对 R 语言提供的算法**RevoScaleR**包。 

通过使用**revoscalepy**，可以创建远程计算上下文、 之间移动数据计算上下文、 转换数据和使用逻辑和线性回归、 决策树之类的常用算法训练预测模型和更多。 有关详细信息，请参阅[SQL Server 中的 revoscalepy 模块](../python/ref-py-revoscalepy.md)并[revoscalepy 函数引用](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)。

1. 在中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，打开一个新**查询**窗口，并运行以下语句以创建存储的过程_TrainTipPredictionModelRxPy_。  由于存储的过程已包含输入数据的定义，因此不需要提供输入的查询。

    ```sql
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    此存储的过程执行的模型定型过程中执行以下步骤：

    - 选择查询应用自定义的标量函数_fnCalculateDistance_计算上车与下车位置之间的直接距离。 查询的结果存储在默认 Python 输入变量`InputDataset`。
    - 二进制变量_tipped_用作*标签*或结果列和模型适合使用这些功能列： _passenger_count_， _trip_距离_， _trip_time_in_secs_，和_direct_distance_。
    - 训练的模型序列化并存储在 Python 变量`logitObj`。 通过添加 T-SQL 关键字输出，可以将变量添加作为存储过程的输出。 在下一步中，该变量用于将模型的二进制代码插入到数据库表_nyc_taxi_models_。 此机制可以轻松地存储和重复使用模型。

2. 运行存储的过程，如下所示，若要插入训练**revoscalepy**插入表模型*nyc_taxi_models*。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    数据处理和模型调整可能需要一段时间。 将其通过管道传递到 Python 的消息**stdout**流显示在**消息**窗口中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 例如：

    *来自外部脚本的 STDOUT 消息：*
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 打开表 nyc_taxi_models。 可以看到已添加了一个新行，在列 _model_中包含序列化模型。

    *revoscalepy_model* *0x8003637265766F7363616c....*

在下一步，使用训练的模型创建预测。

## <a name="next-step"></a>下一步

[运行使用 Python 在存储过程中嵌入的预测](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一步

[使用 T-SQL 创建数据功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)
