---
title: 有关 R 和 SQL 数据类型和对象的 SQL Server 机器学习的快速入门
description: 在本快速入门教程，了解如何使用数据类型与 R 和 SQL Server 中的数据对象。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: df1c4c50e21ba5db5459da958f915be560500dc7
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046771"
---
# <a name="quickstart-handle-data-types-and-objects-using-r-in-sql-server"></a>快速入门：处理数据类型和对象在 SQL Server 中使用 R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入门，获取 R 和 SQL Server 之间移动数据时出现的常见问题的动手介绍。 使用您自己的脚本中的数据时，通过此练习中获得的体验提供了基本的背景。

若要了解得更清楚的常见问题包括：

+ 数据类型有时不匹配
+ 隐式转换可能会发生
+ 有时需要执行强制转换和转换操作
+ R 和 SQL 使用不同的数据对象

## <a name="prerequisites"></a>先决条件

上一个快速入门中， [SQL Server 中存在验证 R](quickstart-r-verify.md)、 提供的信息和链接设置为本快速入门所需的 R 环境。

## <a name="always-return-a-data-frame"></a>始终返回数据帧

当脚本将结果从 R 返回给 SQL Server 时，必须以 **data.frame** 的形式返回数据。 如果你想要输出为存储的过程结果的一部分，任何其他类型的对象，无论它是列表、 因子、 向量或二进制数据-在脚本中的生成必须转换成数据帧。 幸运的是，有多个 R 函数支持将其他对象更改为数据框架。 你甚至可以序列化二进制模型并在数据框架中返回该模型。本教程稍后将介绍此操作。

首先，让我们试着某些 R 基本 R 对象的向量、 矩阵和列表-并请参阅如何转换成数据帧更改传递到 SQL Server 的输出。

比较在 R 中的这两个"Hello World"脚本脚本看上去大致相同，但第一个返回三个值的单个列，而第二个返回三个列具有单个值每个。

**示例 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**示例 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identify-schema-and-data-types"></a>标识架构和数据类型

结果为何有这么大的差别？ 

使用 R `str()` 命令通常可以找到答案。 在 R 脚本中的任何位置添加函数 `str(object_name)` 可使指定 R 对象的数据架构作为信息性消息返回。 若要查看消息，请查看 Visual Studio Code 中的“消息”窗格，或者查看 SSMS 中的“消息”选项卡。

若要找出示例 1 和示例 2 的结果为何有这么大的差别，请在每个语句的 _@script_ 变量定义末尾插入 `str(OutputDataSet)` 行，如下所示：

**添加使用 str 函数的示例 1**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**添加使用 str 函数的示例 2**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

现在，查看“消息”中的文本，了解输出为何不相同的原因。

**结果 - 示例 1**

```sql
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**结果 - 示例 2**

```sql
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

可以看到，对 R 语法进行轻微的更改会给结果的架构造成很大的影响。 我们不会深究原因，但 R 数据类型的差异中的详细信息中所述*数据结构*主题中[由 Hadley wickham 编写的"Advanced R"](http://adv-r.had.co.nz)。

暂时，你只需在将 R 对象强制转换成数据框架时注意检查预期的结果。

> [!TIP]
> 此外可以使用 R 标识函数，如`is.matrix`， `is.vector`，以返回有关内部数据结构的信息。

## <a name="implicit-conversion-of-data-objects"></a>数据对象的隐式转换

每个 R 数据对象都有自身的规则，指定在将值与其他数据对象组合时，如果两个数据对象具有相同的维度数目，或者如果任意数据对象包含异构数据类型，应如何处理值。

例如，假设你要运行以下语句以使用。 执行矩阵乘法具有三个值的单列矩阵乘以包含四个值的数组，因此期望 4x3 矩阵。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

在幕后，包含三个值的列将转换为单列矩阵。 由于矩阵只是 R 中数组的特殊表示形式，数组 `y` 将隐式强制转换为单列矩阵，使这两个参数相符。

**结果**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

但请注意更改数组的大小会发生什么情况`y`。

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

现在，R 返回单个值作为结果。

**结果**
    
|Col1|
|---|
|1542|

原因是什么？ 在这种情况下，两个参数可以为相同长度的向量进行处理，因为 R 将以矩阵形式返回内部乘积。  根据线性代数的规则，这种行为符合预期；但是，如果下游应用程序预期输出架构永远不变，则这种行为可能会导致问题！

> [!TIP]
> 
> 收到错误？ 这些示例要求表**RTestData**。 如果尚未创建测试数据表，请返回到本主题并创建表：[处理输入和输出](../tutorials/rtsql-working-with-inputs-and-outputs.md)。
> 
> 如果你已创建表，但仍收到错误，请确保在包含数据库的表，而不是在上下文中运行存储的过程**主**或另一个数据库。
> 
> 此外，我们建议您不要使用临时表，这些示例。 某些 R 客户端将终止批处理，删除临时表之间的连接。

## <a name="merge-or-multiply-columns-of-different-length"></a>对不同长度的列进行合并或相乘

R 提供了极大的灵活性，使用矢量不同的大小，以及将这些类似于列的结构组合成数据帧。 向量列表可能看起来像表，但它们并不遵循控制数据库表的所有规则。

例如，以下脚本定义长度为 6 的数字数组，并将其存储在 R 变量 `df1` 中。 该数值数组然后组合与整数的 RTestData 表，其中包含三 （3） 值，以使新的数据帧`df2`。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

为了填充数据框架，R 将以所需的次数重复从 RTestData 检索的元素，以匹配数组 `df1` 中的元素数目。

**结果**
    
|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

请记住，数据框架只是看起来像表，但实际上是向量列表。

## <a name="cast-or-convert-sql-server-data"></a>强制转换或转换 SQL Server 数据

R 和 SQL Server 使用的数据类型不同，因此，如果你在 SQL Server 中运行查询来获取数据，然后将该数据传递给 R 运行时，通常会发生某种类型的隐式转换。 将数据从 R 返回到 SQL Server 时，会发生另一套转换。

- SQL Server 将数据从查询推送到快速启动板服务管理的 R 进程，并将其转换为更高的效率的内部表示形式。
- R 运行时将数据加载到 data.frame 变量中，并对数据执行其自身的操作。
- 数据库引擎使用受保护的内部连接将数据返回到 SQL Server，并以 SQL Server 数据类型呈现数据。
- 若要获取数据，可以使用能够发出 SQL 查询并处理表格数据集的客户端或网络库连接到 SQL Server。 此客户端应用程序可能会通过其他方式影响数据。

若要阐释其工作方式上, 运行的查询类似于本[AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)数据仓库。 此视图返回用于创建预测的销售数据。

```sql
USE AdventureWorksDW
GO

SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> 可以使用任何版本的 AdventureWorks，也可以创建不同的查询使用你自己的数据库。 要点是尝试处理一些包含文本、 日期时间和数字值的数据。

现在，请将此查询粘贴作为存储过程的输入。

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

如果遇到错误，可能需要对查询文本进行一些编辑。 例如，必须用两组单引号将 WHERE 子句中的字符串谓词括起来。

正常运行查询后，请查看 `str` 函数的结果，了解 R 如何处理输入数据。

**结果**

```sql
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ 日期时间列已使用 R 数据类型 **POSIXct** 进行处理。
+ 已标识为"ProductSeries"的文本列**身份**，这意味着一个分类变量。 默认情况下，字符串值将作为因子处理。 如果将某个字符串传递给 R，该字符串将转换为整数供内部使用，然后映射回到输出中的字符串。

### <a name="summary"></a>总结

从这些简短的示例，可以看到需要传递 SQL 查询中用作输入时，检查数据转换的效果。 因为某些 SQL Server 数据类型不受 R，请考虑这些方法，从而避免发生错误：

+ 提前测试你的数据并验证列或架构中可能存在问题时传递给 R 代码中的值。
+ 在输入数据源中单独指定列而不要使用 `SELECT *`，并知道如何处理每个列。
+ 准备输入数据时请根据需要执行显式强制转换，避免出现意外。
+ 避免传递列的数据 （如 GUID 或 rowguid） 会导致错误并不是适用于建模。

有关支持的和不受支持的数据类型的详细信息，请参阅[R 库和数据类型](../r/r-libraries-and-data-types.md)。

有关的运行时将字符串转换为数字因子对性能的影响的信息，请参阅[SQL Server R Services 性能优化](../r/sql-server-r-services-performance-tuning.md)。

## <a name="next-step"></a>下一步

在下一步的快速入门中，将了解如何将 R 函数应用到 SQL Server 数据。

> [!div class="nextstepaction"]
> [快速入门：SQL Server 数据使用 R 函数](quickstart-r-functions.md)
