---
title: ScannerState 要素
description: 必要な ScannerState 要素は、デバイスのスキャンのスキャンの部分の現在の状態を識別します。
ms.assetid: 64cd5319-a52d-4ff3-976c-060886381d11
keywords:
- ScannerState 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5a7268352d44d6b2f012dcaaa5d41020aa57d32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370049"
---
# <a name="scannerstate-element"></a>ScannerState 要素


必要な**ScannerState**要素は、デバイスのスキャンのスキャンの部分の現在の状態を識別します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerState>
  text
</wscn:ScannerState>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 次の文字列値の 1 つ。

| 値      | 説明                                                  |
|------------|--------------------------------------------------------------|
| アイドル       | スキャナーは、使用可能な新しいジョブの処理を開始できます。 |
| 処理 | 現在、スキャナーがジョブを処理しています。                    |
| ［停止］    | ジョブを処理できないし、の介入が必要です。         |

 

## <a name="child-elements"></a>子要素


子要素はありません。

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

<a name="remarks"></a>注釈
-------

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

WSD スキャン サービスでは、スキャナーの状態の変更点について、クライアントを通知を送信して、 [ **ScannerStatusSummaryEvent** ](scannerstatussummaryevent.md)イベント。 クライアントは直接呼び出すことによって、スキャナーの状態をクエリ、 [ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作。

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStatus**](scannerstatus.md)

[**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

[**StatusSummary**](statussummary.md)

 

 






