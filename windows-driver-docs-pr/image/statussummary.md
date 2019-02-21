---
title: StatusSummary 要素
description: 必要な StatusSummary 要素には、デバイスのスキャンの現在の状態の概要が含まれています。
ms.assetid: cb361b3b-bd73-449d-9f31-0c1aea882330
keywords:
- StatusSummary 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn StatusSummary
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d62094720d99017ad9597c84ad3b7f3d24224c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560693"
---
# <a name="statussummary-element"></a>StatusSummary 要素


必要な**StatusSummary**要素には、スキャン デバイスの現在の状態の概要が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:StatusSummary>
  child elements
</wscn:StatusSummary>
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
<td><p><a href="scannerstate.md" data-raw-source="[&lt;strong&gt;ScannerState&lt;/strong&gt;](scannerstate.md)"><strong>ScannerState</strong></a></p></td>
</tr>
<tr class="even">
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
<td><p><a href="scannerstatussummaryevent.md" data-raw-source="[&lt;strong&gt;ScannerStatusSummaryEvent&lt;/strong&gt;](scannerstatussummaryevent.md)"><strong>ScannerStatusSummaryEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスを含める必要があります、 **StatusSummary**要素を送信するとき、 [ **ScannerStatusSummaryEvent** ](scannerstatussummaryevent.md)クライアントに event 要素。 スキャナーの現在の状態と理由がこの状態の理由がで指定された、 [ **ScannerState** ](scannerstate.md)と[ **ScannerStateReasons** ](scannerstatereasons.md)要素では、それぞれします。

## <a name="see-also"></a>関連項目


[**ScannerStateReasons**](scannerstatereasons.md)

[**ScannerState**](scannerstate.md)

**ScannerStateReasons**
[**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

 

 






