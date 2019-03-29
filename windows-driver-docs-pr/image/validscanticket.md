---
title: ValidScanTicket 要素
description: 省略可能な ValidScanTicket 要素には、有効な ScanTicket が含まれています。
ms.assetid: 306b5d90-068f-4b63-9155-8f35c7825f16
keywords:
- ValidScanTicket 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ValidScanTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8823a98372fc413a795177c9c5e8ed403a31cdb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573061"
---
# <a name="validscanticket-element"></a>ValidScanTicket 要素


省略可能な**ValidScanTicket**要素が含まれていますが、有効な[ **ScanTicket**](scanticket.md)します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ValidScanTicket>
  child elements
</wscn:ValidScanTicket>
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
<td><p><a href="validationinfo.md" data-raw-source="[&lt;strong&gt;ValidationInfo&lt;/strong&gt;](validationinfo.md)"><strong>ValidationInfo</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

クライアントが送信する、 [ **ScanTicket** ](scanticket.md)を通じて検証、 [ **ValidateScanTicketRequest** ](validatescanticketrequest.md)操作。 場合、送信された**ScanTicket** WSD スキャン サービスが返す必要があります、無効な設定が含まれています、 **ValidScanTicket**要素が有効な設定を無効な設定が変更されることができます。 検証情報を返しますスキャン サービス**ValidScanTicket**の[ **ValidateScanTicketResponse**](validatescanticketresponse.md)します。

## <a name="see-also"></a>関連項目


[**DocumentParameters**](documentparameters.md)

[**JobDescription**](jobdescription.md)

[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

[**ValidationInfo**](validationinfo.md)

 

 






