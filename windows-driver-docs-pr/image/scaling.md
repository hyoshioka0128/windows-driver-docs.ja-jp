---
title: スケーリング要素
description: 省略可能なスケール要素は、スキャンしたドキュメントの高さと幅のスケールを指定します。
ms.assetid: 43769ebf-f883-418a-a0b3-87d5b23601f9
keywords:
- 要素のイメージング デバイスのスケーリング
topic_type:
- apiref
api_name:
- wscn Scaling wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7791a9ab6be968766e2fa873c5ee233758809d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381546"
---
# <a name="scaling-element"></a>スケーリング要素


省略可能な**スケーリング**要素は、スキャンしたドキュメントの高さと幅のスケールを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Scaling wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:Scaling wscn:MustHonor="">
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
<td><p><a href="scalingheight.md" data-raw-source="[&lt;strong&gt;ScalingHeight&lt;/strong&gt;](scalingheight.md)"><strong>ScalingHeight</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scalingwidth.md" data-raw-source="[&lt;strong&gt;ScalingWidth&lt;/strong&gt;](scalingwidth.md)"><strong>ScalingWidth</strong></a></p></td>
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

**スケーリング**要素は、両方を含める必要があります、 [ **ScalingWidth** ](scalingwidth.md)と[ **ScalingHeight** ](scalingheight.md)要素。 **ScalingWidth**要素は、高速スキャンの方向にスケーリングを指定します、 **ScalingHeight**要素は、低速スキャン方向にスケーリングを指定します。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、**スケーリング**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**ScalingHeight**](scalingheight.md)

[**ScalingWidth**](scalingwidth.md)

 

 






