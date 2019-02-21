---
title: RequestedElements 要素
description: 必要な RequestedElements 要素は、GetScannerElementsRequest または GetJobElementsRequest を呼び出すときに、クライアント要求のデータ要素を識別します。
ms.assetid: 0023afc1-723d-4b6a-9f1a-0bc21a309a65
keywords:
- RequestedElements 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn RequestedElements
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414b47dd5bf9aadf6beb7d9c4056d23bdfa4002c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528988"
---
# <a name="requestedelements-element"></a>RequestedElements 要素


必要な**RequestedElements**要素は、クライアントの呼び出し時にデータを必要がある要素を識別します[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)または[。**GetJobElementsRequest**](getjobelementsrequest.md)します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:RequestedElements>
  child elements
</wscn:RequestedElements>
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
<td><p><a href="name-for-requestedelements-element.md" data-raw-source="[&lt;strong&gt;Name for RequestedElements Element&lt;/strong&gt;](name-for-requestedelements-element.md)"><strong>RequestedElements 要素の名前</strong></a></p></td>
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
<td><p><a href="getjobelementsrequest.md" data-raw-source="[&lt;strong&gt;GetJobElementsRequest&lt;/strong&gt;](getjobelementsrequest.md)"><strong>GetJobElementsRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="getscannerelementsrequest.md" data-raw-source="[&lt;strong&gt;GetScannerElementsRequest&lt;/strong&gt;](getscannerelementsrequest.md)"><strong>GetScannerElementsRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**RequestedElements**要素は、1 つ以上含まれています。**名前**要素の親**RequestedElements**クライアントを照会しているデータを識別する要素。

## <a name="see-also"></a>関連項目


[**GetJobElementsRequest**](getjobelementsrequest.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**RequestedElements 要素の名前**](name-for-requestedelements-element.md)

 

 






