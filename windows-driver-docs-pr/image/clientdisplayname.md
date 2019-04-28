---
title: ClientDisplayName 要素
description: 必要な ClientDisplayName 要素には、スキャナーは、そのユーザー インターフェイスで表示する文字列を指定します。
ms.assetid: e43e5c51-5f8e-47af-b5da-707b89401935
keywords:
- ClientDisplayName 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ClientDisplayName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 252523edba3eea7350b9a096c0b9b5ee50df5d7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373197"
---
# <a name="clientdisplayname-element"></a>ClientDisplayName 要素


必要な**ClientDisplayName**要素は、スキャナーは、そのユーザー インターフェイスで表示する文字列を指定します。

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
<td><p><a href="scandestination.md" data-raw-source="[&lt;strong&gt;ScanDestination&lt;/strong&gt;](scandestination.md)"><strong>ScanDestination</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

表示名は、ユーザーがスキャン先として要求元のクライアントを選択できます。 WSD スキャン サービスは、送信、ユーザーはこの表示名を選択し、[スキャン] ボタンを押す、する場合、 [ **ScanAvailableEvent** ](scanavailableevent.md)受信をサブスクライブしてスキャン先にイベント。

## <a name="see-also"></a>関連項目


[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestination**](scandestination.md)

 

 






