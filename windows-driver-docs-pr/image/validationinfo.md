---
title: ValidationInfo 要素
description: 必要な ValidationInfo 要素には、クライアントの ValidateScanTicketRequest への応答内のすべての ScanTicket 検証情報が含まれています。
ms.assetid: c727cbd7-6da0-4750-b36e-3b65e56015fa
keywords:
- ValidationInfo 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ValidationInfo
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c6dd42552ec29116bdcd47a0bea3117c4c7b012
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354863"
---
# <a name="validationinfo-element"></a>ValidationInfo 要素


必要な**ValidationInfo**要素がすべて含まれています[ **ScanTicket** ](scanticket.md)で応答をクライアントの検証情報[ **ValidateScanTicketRequest**](validatescanticketrequest.md)します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ValidationInfo>
  child elements
</wscn:ValidationInfo>
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
<td><p><a href="imageinformation.md" data-raw-source="[&lt;strong&gt;ImageInformation&lt;/strong&gt;](imageinformation.md)"><strong>ImageInformation</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="validscanticket.md" data-raw-source="[&lt;strong&gt;ValidScanTicket&lt;/strong&gt;](validscanticket.md)"><strong>ValidScanTicket</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="validticket.md" data-raw-source="[&lt;strong&gt;ValidTicket&lt;/strong&gt;](validticket.md)"><strong>ValidTicket</strong></a></p></td>
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
<td><p><a href="validatescanticketresponse.md" data-raw-source="[&lt;strong&gt;ValidateScanTicketResponse&lt;/strong&gt;](validatescanticketresponse.md)"><strong>ValidateScanTicketResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ValidationInfo**要素には定義する要素が含まれて かどうか、クライアントの[ **ScanTicket** ](scanticket.md)が有効では、WSD スキャン サービスの変更にどのようなデータそうでない場合、チケットが無効です。 スキャン サービスには、この情報が返されます。 その[ **ValidateScanTicketResponse** ](validatescanticketresponse.md)操作。

## <a name="see-also"></a>関連項目


[**ImageInformation**](imageinformation.md)

[**ScanTicket**](scanticket.md)

[**ValidScanTicket**](validscanticket.md)

[**ValidTicket**](validticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

 

 






