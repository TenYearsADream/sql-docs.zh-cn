---
title: 添加记录 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a17e09df7c7235e1361aae79bd89152c290b1bdb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294388"
---
# <a name="adding-records-to-a-recordset"></a>将记录添加到记录集
使用**AddNew**方法创建并初始化新的记录中的现有**记录集**。 可以使用**支持**方法替换**CursorOptionEnum**的值**adAddNew**以验证是否可以将记录添加到当前**记录集**对象。

 调用后**AddNew**方法，新的记录将成为当前记录，并保持最新调用后**更新**方法。 如果**记录集**对象不支持书签，您可能不能访问新记录后，移动到另一条记录。 因此，具体取决于游标类型，您可能需要调用**再次查询**方法，以便可以访问新的记录。

 如果您调用**AddNew** ADO 编辑当前记录或添加新记录时，调用**更新**方法以保存任何更改，然后创建新记录。

 本部分包含以下主题。

-   [使用 AddNew 添加记录](../../../ado/guide/data/adding-records-using-addnew.md)

-   [添加多个字段](../../../ado/guide/data/adding-multiple-fields.md)

-   [确定编辑模式](../../../ado/guide/data/determining-edit-mode.md)

-   [以即时和批处理模式使用 AddNew](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
