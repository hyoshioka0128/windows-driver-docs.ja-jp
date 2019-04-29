---
title: ClientContext 要素
description: 必要な ClientContext 要素には、クライアント固有の文字列を指定します。
ms.assetid: 09bc5f5b-6198-4553-9f6f-8219e620f634
keywords:
- ClientContext 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ClientDisplayName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 066bcbcfd99348610b9c2dd1b41bf0ca8d5b916d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373186"
---
# <a name="clientcontext-element"></a>ClientContext 要素


必要な**ClientContext**要素は、クライアント固有の文字列を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ClientDisplayName>
  text
</wscn:ClientDisplayName>
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
<td><p><a href="destinationresponse.md" data-raw-source="[&lt;strong&gt;DestinationResponse&lt;/strong&gt;](destinationresponse.md)"><strong>DestinationResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanavailableevent.md" data-raw-source="[&lt;strong&gt;ScanAvailableEvent&lt;/strong&gt;](scanavailableevent.md)"><strong>ScanAvailableEvent</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scandestination.md" data-raw-source="[&lt;strong&gt;ScanDestination&lt;/strong&gt;](scandestination.md)"><strong>ScanDestination</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

ときの親要素、 **ClientContext**要素は[ **ScanDestination**](scandestination.md)、 **ClientContext**する文字列値を指定します。クライアントは提供中に、  **&lt;wse: サブスクライブ&gt;** を受信する要求[ **ScanAvailableEvent** ](scanavailableevent.md)イベント。

親要素の場合は[ **DestinationResponse**](destinationresponse.md)、 **ClientContext**クライアントが subscribe 操作で送信するデータのコピーです。 WSD スキャン サービスでは、このコピーを返します**&lt;wse:SubscribeResponse&gt;** ときに、クライアントのサブスクリプション要求に応答します。

親要素の場合は[ **ScanAvailableEvent**](scanavailableevent.md)、 **ClientContext**文字列値の一部として受信するスキャナーを含む、 **ScanAvailableEvent**サブスクリプション要求。 この文字列により、クライアントに関連付ける、 **ScanAvailableEvent**スキャナーが適切なデバイスとサービス。

 **&lt;Wse: サブスクライブ&gt;** と**&lt;wse:SubscribeResponse&gt;** 要素は、仕様で説明します。

## <a name="see-also"></a>関連項目


[**DestinationResponse**](destinationresponse.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






