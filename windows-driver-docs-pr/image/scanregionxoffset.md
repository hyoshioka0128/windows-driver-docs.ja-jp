---
title: ScanRegionXOffset 要素
description: 省略可能な ScanRegionXOffset 要素には、高速スキャン潜在顧客のエッジからスキャン領域の先頭までの距離を指定します。
ms.assetid: 79123dd1-8532-45a8-a7c5-b6c36ef0baae
keywords:
- ScanRegionXOffset 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScanRegionXOffset wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78b4dc536cdb955e11180ed1fb6ebf8164b6fdd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560686"
---
# <a name="scanregionxoffset-element"></a>ScanRegionXOffset 要素


省略可能な**ScanRegionXOffset**要素は、高速スキャン潜在顧客のエッジからスキャン領域の先頭までの距離を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScanRegionXOffset wscn:MustHonor=""                        wscn:Override=""                        wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ScanRegionXOffset wscn:MustHonor=""                        wscn:Override=""                        wscn:UsedDefault="">
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
<tr class="even">
<td><p><strong><strong>上書き</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>(省略可能)。 ブール値 false、0 にする必要がある、1 または true です。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

必須。 0 ~ InputSize 幅の整数。[ **InputSize**](inputsize.md)

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
<td><p><a href="scanregion.md" data-raw-source="[&lt;strong&gt;ScanRegion&lt;/strong&gt;](scanregion.md)"><strong>ScanRegion</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

スキャンの地域のパラメーターの詳細については、[ **ScanRegion**](scanregion.md)を参照してください。

クライアントは、省略可能な指定できます**MustHonor**属性の場合にのみ、 **ScanRegionXOffset**要素に含まれる、 **CreateScanJobRequest**階層。 詳細については**MustHonor**と使用状況を参照してください[ **CreateScanJobRequest**](createscanjobrequest.md)します。

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、 **ScanRegionXOffset** 内の要素が含まれている**DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**InputSize**](inputsize.md)

[**ScanRegion**](scanregion.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

 

 






