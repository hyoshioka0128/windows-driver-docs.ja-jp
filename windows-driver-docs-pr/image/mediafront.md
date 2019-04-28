---
title: MediaFront 要素
description: 必要な MediaFront 要素には、物理メディアの正面のスキャンに固有のすべてのパラメーターが含まれています。
ms.assetid: 1bde587b-4057-4368-b075-c22561ee45cc
keywords:
- MediaFront 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn MediaFront
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cf7082d4a2693be3830c7962fcb8a3b09b337f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380351"
---
# <a name="mediafront-element"></a>MediaFront 要素


必要な**MediaFront**要素には、物理メディアの正面のスキャンに固有のすべてのパラメーターが含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:MediaFront>
  child elements
</wscn:MediaFront>
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
<td><p><a href="colorprocessing.md" data-raw-source="[&lt;strong&gt;ColorProcessing&lt;/strong&gt;](colorprocessing.md)"><strong>ColorProcessing</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="resolution.md" data-raw-source="[&lt;strong&gt;Resolution&lt;/strong&gt;](resolution.md)"><strong>解決方法</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanregion.md" data-raw-source="[&lt;strong&gt;ScanRegion&lt;/strong&gt;](scanregion.md)"><strong>ScanRegion</strong></a></p></td>
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
<td><p><a href="mediasides.md" data-raw-source="[&lt;strong&gt;MediaSides&lt;/strong&gt;](mediasides.md)"><strong>MediaSides</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

場合、 **MediaFront**要素が含まれていない、 [ **ScanRegion** ](scanregion.md)要素、WSD スキャン サービスが使用 0 オフセットおよび幅と高さのとして、 [**InputMediaSize**](inputmediasize.md)、指定した場合。 場合**ScanRegion**がないと**InputMediaSize**が指定されていないかによって判断できないデバイスのスキャン、実装を指定できます。

## <a name="see-also"></a>関連項目


[**ColorProcessing**](colorprocessing.md)

[**InputMediaSize**](inputmediasize.md)

[**MediaBack**](mediaback.md)

[**MediaSides**](mediasides.md)

[**解決方法**](resolution.md)

[**ScanRegion**](scanregion.md)

 

 






