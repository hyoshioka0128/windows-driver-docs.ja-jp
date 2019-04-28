---
title: ADFBack 要素
description: 省略可能な ADFBack 要素には、スキャナーに接続されている双方向の自動ドキュメント フィーダー (ADF) の裏側の機能について説明します。
ms.assetid: f364c001-ec1a-4f8c-b25a-eaa5368ba05f
keywords:
- ADFBack 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ADFBack
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 760b290d234886706ff5de66e3d3d889dc64c515
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367076"
---
# <a name="adfback-element"></a>ADFBack 要素


省略可能な**ADFBack**要素が、スキャナーに接続されている双方向の自動ドキュメント フィーダー (ADF) の裏側の機能について説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ADFBack>
  child elements
</wscn:ADFBack>
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
<td><p><a href="adfcolor.md" data-raw-source="[&lt;strong&gt;ADFColor&lt;/strong&gt;](adfcolor.md)"><strong>ADFColor</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adfmaximumsize.md" data-raw-source="[&lt;strong&gt;ADFMaximumSize&lt;/strong&gt;](adfmaximumsize.md)"><strong>ADFMaximumSize</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="adfminimumsize.md" data-raw-source="[&lt;strong&gt;ADFMinimumSize&lt;/strong&gt;](adfminimumsize.md)"><strong>ADFMinimumSize</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adfopticalresolution.md" data-raw-source="[&lt;strong&gt;ADFOpticalResolution&lt;/strong&gt;](adfopticalresolution.md)"><strong>ADFOpticalResolution</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="adfresolutions.md" data-raw-source="[&lt;strong&gt;ADFResolutions&lt;/strong&gt;](adfresolutions.md)"><strong>ADFResolutions</strong></a></p></td>
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
<td><p><a href="adf.md" data-raw-source="[&lt;strong&gt;ADF&lt;/strong&gt;](adf.md)"><strong>ADF</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスを指定する必要があります、 **ADFBack**要素とその子スキャナーの ADF の二重化をサポートする場合のみです。

## <a name="see-also"></a>関連項目


[**ADF**](adf.md)

[**ADFColor**](adfcolor.md)

[**ADFMaximumSize**](adfmaximumsize.md)

[**ADFMinimumSize**](adfminimumsize.md)

[**ADFOpticalResolution**](adfopticalresolution.md)

[**ADFResolutions**](adfresolutions.md)

 

 






