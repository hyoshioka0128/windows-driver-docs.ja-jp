---
title: ValidTicket 要素
description: 必要な ValidTicket 要素は、クライアントの ScanTicket が有効かどうかを示します。
ms.assetid: 8c2f35b5-1b1e-49a4-8aab-4d57ff9f1803
keywords:
- ValidTicket 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ValidTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62cce5fb77d4c10f1da4d1ea5c23129cba95c512
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356133"
---
# <a name="validticket-element"></a>ValidTicket 要素


必要な**ValidTicket**要素を示すかどうか、クライアントの[ **ScanTicket** ](scanticket.md)が無効です。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ValidTicket>
  text
</wscn:ValidTicket>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 ブール値 false、0 にする必要がある、1 または true です。

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
<td><p><a href="validationinfo.md" data-raw-source="[&lt;strong&gt;ValidationInfo&lt;/strong&gt;](validationinfo.md)"><strong>ValidationInfo</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントが送信する、 [ **ScanTicket** ](scanticket.md)を通じて検証、 [ **ValidateScanTicketRequest** ](validatescanticketrequest.md)操作。 WSD スキャン サービスが含まれる検証情報を返します**ValidTicket**の[ **ValidateScanTicketResponse**](validatescanticketresponse.md)します。

## <a name="see-also"></a>関連項目


[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidateScanTicketResponse**](validatescanticketresponse.md)

[**ValidationInfo**](validationinfo.md)

 

 






