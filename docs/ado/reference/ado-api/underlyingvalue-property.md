---
title: UnderlyingValue 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7bcb751fb32634fc544dfa11ee862cd47112514
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043502"
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 属性
指示当前的值[字段](../../../ado/reference/ado-api/field-object.md)数据库中的对象。  
  
## <a name="return-value"></a>返回值  
 返回**Variant**值，该值指示的值**字段**。  
  
## <a name="remarks"></a>备注  
 使用**UnderlyingValue**属性，以便从数据库返回当前字段值。 中的字段值**UnderlyingValue**属性是对您的事务可见，并且可能是一个新的更新由其他事务的结果的值。 这可能不同于[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)属性，这反映了最初返回到的值[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 这是类似于使用[重新同步](../../../ado/reference/ado-api/resync-method.md)方法，但**UnderlyingValue**属性将返回从当前记录仅特定字段的值。 这是相同的值，该值[重新同步](../../../ado/reference/ado-api/resync-method.md)方法使用替换[值](../../../ado/reference/ado-api/value-property-ado.md)属性。  
  
 当使用此属性与**OriginalValue**属性，可以解析从批处理更新而引起的冲突。  
  
## <a name="record"></a>录制  
 有关[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，此属性将为空的字段前添加[更新](../../../ado/reference/ado-api/update-method.md)调用。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>请参阅  
 [OriginalValue 和 UnderlyingValue 属性示例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 和 UnderlyingValue 属性示例 （VC + +）](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue 属性 (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)
