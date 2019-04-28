---
title: ADFOpticalResolution 要素
description: 必要な ADFOpticalResolution 要素には、自動ドキュメント フィーダー (ADF) の前または後ろの側をスキャンできます最大解像を指定します。
ms.assetid: 2000dbe4-9733-4a69-9e4e-c53c5a1c24c0
keywords:
- ADFOpticalResolution 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ADFOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2c2e683281d2a3073a4d950a3a78dfee2aa466b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367082"
---
# <a name="adfopticalresolution-element"></a>ADFOpticalResolution 要素


必要な**ADFOpticalResolution**要素を自動ドキュメント フィーダー (ADF) の前または後ろの側をスキャンできます最大光の解像度を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ADFOpticalResolution>
  child elements
</wscn:ADFOpticalResolution>
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>Height</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>幅</strong></a></p></td>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

として解像度が指定されて、 [**幅**](width.md) × [**高さ**](height.md)のペアを両方**幅**と**高さ**1 インチあたりのピクセル単位で指定されます。

場合の親要素、 **ADFOpticalResolution**要素は[ **ADFFront**](adffront.md)前面に指定したの光学解像度が適用されますそれ以外の ADF 側、。親要素が[ **ADFBack** ](adfback.md)と光の解像度は、ADF の背面に適用されます。

## <a name="see-also"></a>関連項目


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**Height**](height.md)

[**幅**](width.md)

 

 






