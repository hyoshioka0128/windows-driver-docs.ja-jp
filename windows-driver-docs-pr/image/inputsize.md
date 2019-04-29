---
title: InputSize 要素
description: 省略可能な InputSize 要素には、スキャンの元のメディアのサイズを指定します。
ms.assetid: 406cfff9-7357-467f-a07a-340e32d9220f
keywords:
- InputSize 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn InputSize wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c983a30712fd93c9e31f275cc14e9a3b0af40b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326079"
---
# <a name="inputsize-element"></a>InputSize 要素


省略可能な**InputSize**要素は、スキャンの元のメディアのサイズを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:InputSize wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:InputSize wscn:MustHonor="">
```

<a name="attributes"></a>属性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="documentsizeautodetect.md" data-raw-source="[&lt;strong&gt;DocumentSizeAutoDetect&lt;/strong&gt;](documentsizeautodetect.md)"><strong>DocumentSizeAutoDetect</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="inputmediasize.md" data-raw-source="[&lt;strong&gt;InputMediaSize&lt;/strong&gt;](inputmediasize.md)"><strong>InputMediaSize</strong></a></p></td>
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
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**InputSize**要素に含めることができます、 [ **DocumentSizeAutoDetect** ](documentsizeautodetect.md)または[ **InputMediaSize** ](inputmediasize.md)要素が両方ではなく、します。 **DocumentSizeAutoDetect**デバイス自動的に元のページのサイズがによって検出されたことを指定します。 **InputMediaSize**現在のジョブをスキャンするメディアのサイズを指定します。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、 **InputSize**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**DocumentSizeAutoDetect**](documentsizeautodetect.md)

[**InputMediaSize**](inputmediasize.md)

 

 






