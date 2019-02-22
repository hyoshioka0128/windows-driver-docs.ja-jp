---
title: ScanTicket 要素
description: 必要な ScanTicket 要素は、識別された現在のスキャン ジョブの説明と処理のパラメーターのすべてを定義します。
ms.assetid: d507bd46-8fc4-49d3-9575-2d83fd7ae625
keywords:
- ScanTicket 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5089696e6c40b81074dcb9e38d92a786e707610f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532351"
---
# <a name="scanticket-element"></a>ScanTicket 要素


必要な**ScanTicket**要素では、すべての識別された現在のスキャン ジョブの説明と処理のパラメーターを定義します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanTicket>
  child elements
</wscn:ScanTicket>
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
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobdescription.md" data-raw-source="[&lt;strong&gt;JobDescription&lt;/strong&gt;](jobdescription.md)"><strong>JobDescription</strong></a></p></td>
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
<td><p><a href="createscanjobrequest.md" data-raw-source="[&lt;strong&gt;CreateScanJobRequest&lt;/strong&gt;](createscanjobrequest.md)"><strong>CreateScanJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>ジョブ</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="validatescanticketrequest.md" data-raw-source="[&lt;strong&gt;ValidateScanTicketRequest&lt;/strong&gt;](validatescanticketrequest.md)"><strong>ValidateScanTicketRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ScanTicket**要素には、クライアントが選択されている現在のジョブのスキャナーの設定の値が含まれています。 クライアントを作成、 **ScanTicket**スキャナーをサポートする値のみを使用しています。 クライアントが呼び出すことによってこのような値を取得、 [ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作とスキャナーを待って[ **DefaultScanTicket** ](defaultscanticket.md)要素。

メンバー要素**ScanTicket**のインスタンスに直接マップ、 [**ジョブ**](job.md)要素、およびそれらが正確に、クライアントは、中に、スキャナーに送信する必要が[ **CreateScanJobRequest** ](createscanjobrequest.md)操作。

クライアントを要求できる、 **ScanTicket**呼び出すことによって特定のジョブの要素。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DefaultScanTicket**](defaultscanticket.md)

[**DocumentParameters**](documentparameters.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ジョブ**](job.md)

[**JobDescription**](jobdescription.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

 

 






