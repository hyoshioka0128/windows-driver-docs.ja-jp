---
title: DestinationToken 要素
description: 必要な DestinationToken 要素には、現在のクライアントの移行先にスキャナーを代入するデバイス固有の文字列が含まれています。
ms.assetid: 92ff99a2-079a-4001-aa01-ff5db09f6fd2
keywords:
- DestinationToken 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DestinationToken
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd3c7643a90b37ff7993fdde5582883ef31cb0d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373180"
---
# <a name="destinationtoken-element"></a>DestinationToken 要素


必要な**DestinationToken**要素には、現在のクライアントの移行先にスキャナーを代入するデバイス固有の文字列が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DestinationToken>
  text
</wscn:DestinationToken>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 任意の有効な文字の文字列。

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
<td><p><a href="createscanjobrequest.md" data-raw-source="[&lt;strong&gt;CreateScanJobRequest&lt;/strong&gt;](createscanjobrequest.md)"><strong>CreateScanJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="destinationresponse.md" data-raw-source="[&lt;strong&gt;DestinationResponse&lt;/strong&gt;](destinationresponse.md)"><strong>DestinationResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントが含まれています、 **DestinationToken**トークンを送信するとき、 [ **CreateScanJobRequest** ](createscanjobrequest.md)操作の要素の後、 [ **ScanAvailableEvent** ](scanavailableevent.md)イベント。 WSD スキャン サービスでは、指定した文字列を使用して、適切なクライアントがスキャン要求を送信することを確認します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DestinationResponse**](destinationresponse.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






