---
title: ConditionHistory 要素
description: 省略可能な ConditionHistory 要素は、スキャナーの最新の状態とエラーの詳細を提供する ConditionHistoryEntry 要素のコレクションです。
ms.assetid: 3725a635-6571-4a34-b8f9-9fe6881bd6da
keywords:
- ConditionHistory 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ConditionHistory
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9c0438c690d72dcbc166f0756b8d3019e3b5ca2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559267"
---
# <a name="conditionhistory-element"></a>ConditionHistory 要素


省略可能な**ConditionHistory**要素のコレクションである[ **ConditionHistoryEntry** ](conditionhistoryentry.md)スキャナーの最新の状態とエラーの詳細を提供する要素.

<a name="usage"></a>使用方法
-----

```xml
<wscn:ConditionHistory>
  child elements
</wscn:ConditionHistory>
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
<td><p><a href="conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;ConditionHistoryEntry&lt;/strong&gt;](conditionhistoryentry.md)"><strong>ConditionHistoryEntry</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
<td><p></p>
<p>ScannerStatus</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

スキャナーの照会できます**ConditionHistory**要素を呼び出すことによって、 [ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作。

条件は、"重大"に情報の重大度によって異なります。

## <a name="see-also"></a>関連項目


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStatus**](scannerstatus.md)

 

 






