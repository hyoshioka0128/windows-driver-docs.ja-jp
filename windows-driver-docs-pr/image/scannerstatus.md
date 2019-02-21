---
title: ScannerStatus 要素
description: 必要な ScannerStatus 要素には、オートマトン (時刻や、スキャナーでの状態の変化) を制御する、スキャナーに関連する情報の現在の状態が含まれています。
ms.assetid: 39a1bbc1-acee-4ac8-8b14-35a3be5076ae
keywords:
- ScannerStatus 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerStatus
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 170782590c948c89b80df049fd8b0533d28c3bed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537388"
---
# <a name="scannerstatus-element"></a>ScannerStatus 要素


必要な**ScannerStatus**オートマトン (時刻や、スキャナーでの状態の変化) を制御する、スキャナーに関連する情報の現在の状態を格納する要素。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerStatus>
  child elements
</wscn:ScannerStatus>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="activeconditions.md" data-raw-source="[&lt;strong&gt;ActiveConditions&lt;/strong&gt;](activeconditions.md)"><strong>ActiveConditions</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="conditionhistory.md" data-raw-source="[&lt;strong&gt;ConditionHistory&lt;/strong&gt;](conditionhistory.md)"><strong>ConditionHistory</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scannercurrenttime.md" data-raw-source="[&lt;strong&gt;ScannerCurrentTime&lt;/strong&gt;](scannercurrenttime.md)"><strong>ScannerCurrentTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scannerstate.md" data-raw-source="[&lt;strong&gt;ScannerState&lt;/strong&gt;](scannerstate.md)"><strong>ScannerState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scannerstatereasons.md" data-raw-source="[&lt;strong&gt;ScannerStateReasons&lt;/strong&gt;](scannerstatereasons.md)"><strong>ScannerStateReasons</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="elementdata-for-scannerelements-element.md" data-raw-source="[&lt;strong&gt;ElementData Element for ScannerElements&lt;/strong&gt;](elementdata-for-scannerelements-element.md)"><strong>ScannerElements ElementData 要素</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ActiveConditions**](activeconditions.md)

[**ConditionHistory**](conditionhistory.md)

[**ScannerElements ElementData 要素**](elementdata-for-scannerelements-element.md)

[**ScannerCurrentTime**](scannercurrenttime.md)

[**ScannerState**](scannerstate.md)

[**ScannerStateReasons**](scannerstatereasons.md)

 

 






