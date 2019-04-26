---
title: FilmScanModeValue 要素
description: 必要な FilmScanModeValue 要素は、フィルムをスキャン オプションをサポートする特定のフィルム露出型を識別します。
ms.assetid: 62d72190-f1c5-4b2f-af6a-a3c530cc51ed
keywords:
- FilmScanModeValue 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FilmScanModeValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9435d1dc06ef9147e22444d4479dfc9c4d110fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358038"
---
# <a name="filmscanmodevalue-element"></a>FilmScanModeValue 要素


必要な**FilmScanModeValue**要素は、フィルムをスキャン オプションをサポートする特定のフィルム露出型を識別します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FilmScanModeValue>
  text
</wscn:FilmScanModeValue>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 次のいずれかの値です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="NotApplicable"></span><span id="notapplicable"></span><span id="NOTAPPLICABLE"></span>NotApplicable</p></td>
<td><p>既定のスキャンの入力ソースは、フィルム オプションでは; ではなくなりましたそのため、FilmScanModeValue は DefaultScanTicket 要素の該当する値ではなくなりました。 NotApplicable は DefaultScanTicket 要素でのみ有効です。</p></td>
</tr>
<tr class="even">
<td><p><span id="ColorSlideFilm"></span><span id="colorslidefilm"></span><span id="COLORSLIDEFILM"></span>ColorSlideFilm</p></td>
<td><p>フィルムの画像は、通常の色空間です。</p></td>
</tr>
<tr class="odd">
<td><p><span id="ColorNegativeFilm"></span><span id="colornegativefilm"></span><span id="COLORNEGATIVEFILM"></span>ColorNegativeFilm</p></td>
<td><p>フィルムの画像は、通常の色空間の陰性の数です。</p></td>
</tr>
<tr class="even">
<td><p><span id="BlackandWhiteNegativeFilm"></span><span id="blackandwhitenegativefilm"></span><span id="BLACKANDWHITENEGATIVEFILM"></span>BlackandWhiteNegativeFilm</p></td>
<td><p>フィルムの画像は、キャプチャしたイメージの白黒陰性の数です。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="filmscanmodessupported.md" data-raw-source="[&lt;strong&gt;FilmScanModesSupported&lt;/strong&gt;](filmscanmodessupported.md)"><strong>FilmScanModesSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**DefaultScanTicket**](defaultscanticket.md)

[**FilmScanModesSupported**](filmscanmodessupported.md)

 

 






