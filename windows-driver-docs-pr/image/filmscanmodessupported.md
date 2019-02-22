---
title: FilmScanModesSupported 要素
description: 必要な FilmScanModesSupported 要素には、フィルムをスキャン オプションをサポートするフィルム危険度の種類の一覧が含まれています。
ms.assetid: bcc1335f-4465-4bc1-a804-b6e8729ec616
keywords:
- FilmScanModesSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FilmScanModesSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf2472a14dbbe96338899781382c13924754b89e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553481"
---
# <a name="filmscanmodessupported-element"></a>FilmScanModesSupported 要素


必要な**FilmScanModesSupported**要素には、フィルムをスキャン オプションをサポートするフィルム危険度の種類の一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FilmScanModesSupported>
  child elements
</wscn:FilmScanModesSupported>
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
<td><p><a href="filmscanmodevalue.md" data-raw-source="[&lt;strong&gt;FilmScanModeValue&lt;/strong&gt;](filmscanmodevalue.md)"><strong>FilmScanModeValue</strong></a></p></td>
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
<td><p><a href="film.md" data-raw-source="[&lt;strong&gt;Film&lt;/strong&gt;](film.md)"><strong>フィルム</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**FilmScanModesSupported**要素は、1 つ以上含まれています。 [ **FilmScanModeValue** ](filmscanmodevalue.md)子要素。 各**FilmScanModeValue**要素は、フィルムをスキャン オプションをサポートするフィルム露出型を識別します。

## <a name="see-also"></a>関連項目


[**フィルム**](film.md)

[**FilmScanModeValue**](filmscanmodevalue.md)

 

 






