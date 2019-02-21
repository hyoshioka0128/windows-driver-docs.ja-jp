---
title: 圧縮されたテクスチャ サーフェス
description: 圧縮されたテクスチャ サーフェス
ms.assetid: 72096a2a-5a4b-4800-bd99-6d403c54889d
keywords:
- 圧縮描画では、WDK DirectDraw をテクスチャ圧縮テクスチャ サーフェスについて
- 圧縮されたテクスチャ サーフェスに関する、DirectDraw 圧縮テクスチャ WDK Windows 2000 の表示します。
- 圧縮されたテクスチャ サーフェス WDK DirectDraw、圧縮されたテクスチャ サーフェスについて
- WDK DirectDraw、圧縮されたテクスチャを表示します。
- 圧縮テクスチャ WDK DirectDraw、
- 描画圧縮テクスチャ WDK DirectDraw
- DirectDraw 圧縮テクスチャ WDK Windows 2000 の表示
- 圧縮されたテクスチャ サーフェスの WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 337c54f5856085967ce86b6b567369a881eba7d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549398"
---
# <a name="compressed-texture-surfaces"></a>圧縮されたテクスチャ サーフェス


## <span id="ddk_compressed_texture_surfaces_gg"></span><span id="DDK_COMPRESSED_TEXTURE_SURFACES_GG"></span>


サーフェスは、3 D オブジェクトのテクスチャに使用されるビットマップを含めることができます。 テクスチャで消費されるメモリ量を減らすためには、Microsoft DirectDraw はテクスチャ サーフェスの圧縮をサポートします。

**注**  圧縮テクスチャ サーフェスをサポートするために新しいコールバックが追加されていません。 DirectDraw では、既存のドライバーのコールバックを使用してドライバー圧縮テクスチャ サーフェスについての情報を渡します。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">FOURCC</th>
<th align="left">説明</th>
<th align="left">アルファ
<div>
 
</div>
前乗算されたでしょうか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXT1</p></td>
<td align="left"><p>非透過/1 ビットのアルファ</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXT2</p></td>
<td align="left"><p>明示的なアルファ</p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXT3</p></td>
<td align="left"><p>明示的なアルファ</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXT4</p></td>
<td align="left"><p>補間されたアルファ</p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXT5</p></td>
<td align="left"><p>補間されたアルファ</p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

上記の 5 種類のドライバーがサポートする圧縮テクスチャを示しています。

圧縮テクスチャ形式の詳細については、次を参照してください。**圧縮テクスチャ形式**DirectDraw SDK のドキュメント。

 

 





