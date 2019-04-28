---
title: ScanDestination 要素
description: 必要な ScanDestination 要素では、クライアントで単一のスキャン変換先を指定します。
ms.assetid: 3cd685b2-36b2-4f28-a80f-a68204631e0c
keywords:
- ScanDestination 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanDestination
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a09785e727e2d1e16102b94ddac5b301b3f66cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364384"
---
# <a name="scandestination-element"></a>ScanDestination 要素


必要な**ScanDestination**要素は、クライアントの単一のスキャン変換先を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanDestination>
  child elements
</wscn:ScanDestination>
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
<td><p><a href="clientcontext.md" data-raw-source="[&lt;strong&gt;ClientContext&lt;/strong&gt;](clientcontext.md)"><strong>ClientContext</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="clientdisplayname.md" data-raw-source="[&lt;strong&gt;ClientDisplayName&lt;/strong&gt;](clientdisplayname.md)"><strong>ClientDisplayName</strong></a></p></td>
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
<td><p><a href="scandestinations.md" data-raw-source="[&lt;strong&gt;ScanDestinations&lt;/strong&gt;](scandestinations.md)"><strong>ScanDestinations</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントは、1 つ以上含まれています。 **ScanDestination**内の要素、 **ScanDestinations**サブスクリプションの作成時に送信する要素。 WSD スキャン サービス内で提供される情報を使用して**ScanDestination**を適切な作成[ **ScanAvailableEvent** ](scanavailableevent.md) event 要素。

## <a name="see-also"></a>関連項目


[**ClientContext**](clientcontext.md)

[**ClientDisplayName**](clientdisplayname.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanDestinations**](scandestinations.md)

 

 






