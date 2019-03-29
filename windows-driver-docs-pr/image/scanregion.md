---
title: ScanRegion 要素
description: 省略可能な ScanRegion 要素では、入力ドキュメントの境界内をスキャンする領域を指定します。
ms.assetid: 29b94df7-503d-4bbd-99a8-9092140c6629
keywords:
- ScanRegion 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanRegion
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3978b3e780aa2a2b778819dceb42ec4dfdbc366
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579433"
---
# <a name="scanregion-element"></a>ScanRegion 要素


省略可能な**ScanRegion**要素は、入力ドキュメントの境界内をスキャンする領域を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanRegion>
  child elements
</wscn:ScanRegion>
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
<td><p><a href="scanregionheight.md" data-raw-source="[&lt;strong&gt;ScanRegionHeight&lt;/strong&gt;](scanregionheight.md)"><strong>ScanRegionHeight</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanregionwidth.md" data-raw-source="[&lt;strong&gt;ScanRegionWidth&lt;/strong&gt;](scanregionwidth.md)"><strong>ScanRegionWidth</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanregionxoffset.md" data-raw-source="[&lt;strong&gt;ScanRegionXOffset&lt;/strong&gt;](scanregionxoffset.md)"><strong>ScanRegionXOffset</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanregionyoffset.md" data-raw-source="[&lt;strong&gt;ScanRegionYOffset&lt;/strong&gt;](scanregionyoffset.md)"><strong>ScanRegionYOffset</strong></a></p></td>
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
<td><p><a href="mediaback.md" data-raw-source="[&lt;strong&gt;MediaBack&lt;/strong&gt;](mediaback.md)"><strong>MediaBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafront.md" data-raw-source="[&lt;strong&gt;MediaFront&lt;/strong&gt;](mediafront.md)"><strong>MediaFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

すべて**ScanRegion**値は 1 つの部分の 1/1000 を表します (1/1000) インチです。

スキャン ジョブの要求されたスキャンの領域は完全にスキャン デバイスの取得がサポートされている領域の外に該当する場合、は、スキャン操作を拒否する必要があります。

[**ScanRegionXOffset**](scanregionxoffset.md) + [**ScanRegionWidth** ](scanregionwidth.md)以下にする必要がありますよりも、 [ **InputSize** ](inputsize.md)幅。

[**ScanRegionYOffset**](scanregionyoffset.md) + [**ScanRegionHeight** ](scanregionheight.md)以下にする必要がありますよりも、 **InputSize**高さ。

WSD スキャン サービスは、指定した寸法を満たすことはできない場合、要求されたスキャンの領域を調整できます。 スキャンのリージョンへの変更を報告するか、 [ **DocumentFinalParameters** ](documentfinalparameters.md)スキャン ジョブ内の要素。

## <a name="see-also"></a>関連項目


[**DocumentFinalParameters**](documentfinalparameters.md)

[**InputSize**](inputsize.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

[**ScanRegionHeight**](scanregionheight.md)

[**ScanRegionWidth**](scanregionwidth.md)

[**ScanRegionXOffset**](scanregionxoffset.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

 

 






