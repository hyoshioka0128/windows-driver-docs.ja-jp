---
title: プラテン要素
description: 省略可能なプラテン要素には、スキャナーで利用可能なフラット ベッドからプラテン上の機能について説明します。
ms.assetid: bda5aa6d-ac19-4af2-9b21-64b29d726e80
keywords:
- プラテン要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn Platen
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de6cb52af56399dee1cd6d0ba67b6a4dd038028
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581878"
---
# <a name="platen-element"></a>プラテン要素


省略可能な**プラテン**要素が、スキャナーで利用可能なフラット ベッドからプラテン上の機能について説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Platen>
  child elements
</wscn:Platen>
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
<td><p><a href="platencolor.md" data-raw-source="[&lt;strong&gt;PlatenColor&lt;/strong&gt;](platencolor.md)"><strong>PlatenColor</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="platenmaximumsize.md" data-raw-source="[&lt;strong&gt;PlatenMaximumSize&lt;/strong&gt;](platenmaximumsize.md)"><strong>PlatenMaximumSize</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenminimumsize.md" data-raw-source="[&lt;strong&gt;PlatenMinimumSize&lt;/strong&gt;](platenminimumsize.md)"><strong>PlatenMinimumSize</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="platenopticalresolution.md" data-raw-source="[&lt;strong&gt;PlatenOpticalResolution&lt;/strong&gt;](platenopticalresolution.md)"><strong>PlatenOpticalResolution</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenresolutions.md" data-raw-source="[&lt;strong&gt;PlatenResolutions&lt;/strong&gt;](platenresolutions.md)"><strong>PlatenResolutions</strong></a></p></td>
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
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

WSD スキャン サービスがすべての構成情報を提供する必要があります、デバイスのスキャンのフラット ベッドからプラテン上にある場合**プラテン**子要素。

## <a name="see-also"></a>関連項目


[**PlatenColor**](platencolor.md)

[**PlatenMaximumSize**](platenmaximumsize.md)

[**PlatenMinimumSize**](platenminimumsize.md)

[**PlatenOpticalResolution**](platenopticalresolution.md)

[**PlatenResolutions**](platenresolutions.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






