---
title: ActiveConditions 要素
description: 必要な ActiveConditions 要素は、現在アクティブな条件またはデバイスのスキャン エラーのすべてのコレクションです。
ms.assetid: e66196af-d794-4ffe-99e5-c0f8ea4ffe74
keywords:
- ActiveConditions 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ActiveConditions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b556ffc0fa4b75b6b2e7639433e5a62af4d573c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549275"
---
# <a name="activeconditions-element"></a>ActiveConditions 要素


必要な**ActiveConditions**要素は、現在アクティブな条件またはデバイスのスキャン エラーのすべてのコレクション。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ActiveConditions>
  child elements
</wscn:ActiveConditions>
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
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
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
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ActiveConditions**要素の一覧は、 [ **DeviceCondition** ](devicecondition.md)すべてのデバイスでエラーまたは現在アクティブな条件を記述する要素。 デバイスの状態は、情報の重大度は"重大"に変更できます。

## <a name="see-also"></a>関連項目


[**DeviceCondition**](devicecondition.md)

[**ScannerStatus**](scannerstatus.md)

 

 






