---
title: DestinationResponses 要素
description: 必要な DestinationResponses 要素は、すべてのクライアントのスキャン対象の要求に応答のコレクションです。
ms.assetid: f373b584-eec9-412e-80b2-3d8a69f4b7ca
keywords:
- DestinationResponses 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DestinationResponses
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eccb08fddbdba327c176428e2f4efffa3ba14d11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373175"
---
# <a name="destinationresponses-element"></a>DestinationResponses 要素


必要な**DestinationResponses**要素は、コレクションのすべてのクライアントのスキャン対象の要求に応答します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DestinationResponses>
  child elements
</wscn:DestinationResponses>
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
<td><p><a href="destinationresponse.md" data-raw-source="[&lt;strong&gt;DestinationResponse&lt;/strong&gt;](destinationresponse.md)"><strong>DestinationResponse</strong></a></p></td>
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
<td><p>&lt;wse:SubscribeResponse&gt;</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスは、いずれかを指定する必要があります[ **DestinationResponse** ](destinationresponse.md)内の子要素を**DestinationResponses**要素ごと[ **ScanDestination** ](scandestination.md)でクライアントを指定する要素を **&lt;wse: サブスクライブ&gt;** 要求。 **&lt;Wse: サブスクライブ&gt;** 要素は、仕様で説明します。

## <a name="see-also"></a>関連項目


[**DestinationResponse**](destinationresponse.md)

[**ScanDestination**](scandestination.md)

 

 






