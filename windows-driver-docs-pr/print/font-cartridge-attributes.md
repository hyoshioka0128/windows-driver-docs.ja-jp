---
title: フォント カートリッジ属性
description: フォント カートリッジ属性
ms.assetid: d1f99322-9c77-428a-beb5-6d0ff166c3e5
keywords:
- WDK Unidrv、カートリッジ プリンターのフォントの記述
- フォントのカートリッジ WDK Unidrv
- カートリッジ フォント WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4072ce5fd3e5f6d5479f451ad6802efda50ebc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363240"
---
# <a name="font-cartridge-attributes"></a>フォント カートリッジ属性





次の表に含まれる属性が含まれています、 \*FontCartridge GPD エントリ。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>属性パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>CartridgeName</strong></p></td>
<td><p>カートリッジの名前を表すテキスト文字列。</p></td>
<td><p>必要な場合を除き、*<strong>rcCartridgeNameID</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>フォント</strong></p></td>
<td><p>カートリッジに含まれている方向を縦長と横長の両方で利用可能なフォントを表す RC_UFM または RC_FONT のリソース識別子の一覧。</p></td>
<td><p>少なくとも 1 つの<em><strong>フォント</strong>、*<strong>PortraitFonts</strong>または *<strong>LandscapeFonts</strong>指定する必要があります。 フォント リソース識別子は、1 から連続番号する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>LandscapeFonts</strong></p></td>
<td><p>横向きでのみ利用可能なカートリッジに含まれているフォントを表す RC_UFM または RC_FONT のリソース識別子の一覧。</p></td>
<td><p>少なくとも 1 つの<em><strong>フォント</strong>、*<strong>PortraitFonts</strong>または *<strong>LandscapeFonts</strong>指定する必要があります。 フォント リソース識別子は、1 から連続番号する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>PortraitFonts</strong></p></td>
<td><p>縦向きでのみ利用可能なカートリッジに含まれているフォントを表す RC_UFM または RC_FONT のリソース識別子の一覧。</p></td>
<td><p>少なくとも 1 つの<em><strong>フォント</strong>、*<strong>PortraitFonts</strong>または *<strong>LandscapeFonts</strong>指定する必要があります。 フォント リソース識別子は、1 から連続番号する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>rcCartridgeNameID</strong></p></td>
<td><p>カートリッジの名前を表す文字列リソースのリソース識別子。</p></td>
<td><p>必要な場合を除き、*<strong>CartridgeName</strong>を指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 




