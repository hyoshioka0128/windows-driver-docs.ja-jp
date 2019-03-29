---
title: ScannerStateReasons 要素
description: 必要な ScannerStateReasons 要素は、すべてのスキャナーが現在の状態である理由を説明する ScannerStateReason 要素の一覧を示します。
ms.assetid: 1b4e6537-4175-4bed-9af3-7887a2737784
keywords:
- ScannerStateReasons 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ff69c1bf009a1dd31f474d949589aa7ef16ffed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573339"
---
# <a name="scannerstatereasons-element"></a>ScannerStateReasons 要素


必要な**ScannerStateReasons**要素の一覧は、 [ **ScannerStateReason** ](scannerstatereason.md)要素をすべてのスキャナーが現在の状態である理由について説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerStateReasons>
  child elements
</wscn:ScannerStateReasons>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

なし

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
<td><p><a href="scannerstatereason.md" data-raw-source="[&lt;strong&gt;ScannerStateReason&lt;/strong&gt;](scannerstatereason.md)"><strong>ScannerStateReason</strong></a></p></td>
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
<tr class="even">
<td><p><a href="statussummary.md" data-raw-source="[&lt;strong&gt;StatusSummary&lt;/strong&gt;](statussummary.md)"><strong>StatusSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

**ScannerStateReasons**要素の一覧は、 **ScannerStateReason**要素、スキャナーが現在の状態である理由をそれぞれについて説明します。

WSD スキャン サービスでは、スキャナーの状態の変更点について、クライアントを通知を送信して、 [ **ScannerStatusSummaryEvent** ](scannerstatussummaryevent.md)イベント。 クライアントは直接呼び出すことによって、スキャナーの状態をクエリ、 [ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作。

## <a name="see-also"></a>関連項目


[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStateReason**](scannerstatereason.md)

[**ScannerStatus**](scannerstatus.md)

[**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

[**StatusSummary**](statussummary.md)

 

 






