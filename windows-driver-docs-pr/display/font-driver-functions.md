---
title: フォント ドライバー関数
description: フォント ドライバー関数
ms.assetid: 95bf5a3b-29f8-43d2-9f24-22cfe257ead4
keywords:
- フォント、WDK グラフィック ドライバー関数
- GDI WDK Windows 2000 の表示、フォント、ドライバー関数
- グラフィック ドライバー WDK Windows 2000 を表示、フォント、ドライバー関数
- DrvLoadFontFile
- DrvUnloadFontFile
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5560ff7b1bdffd5057a3a6fef235db53211fe92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338723"
---
# <a name="font-driver-functions"></a>フォント ドライバー関数


## <span id="ddk_font_driver_functions_gg"></span><span id="DDK_FONT_DRIVER_FUNCTIONS_GG"></span>


前のトピックで説明されている機能だけでなく、次の表には、フォント ドライバーがサポートするその他のいくつかの関数が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556247" data-raw-source="[&lt;strong&gt;DrvLoadFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556247)"><strong>DrvLoadFontFile</strong></a></p></td>
<td align="left"><p>フォントの実現; を作成するために使用するファイルを指定しますドライバーは、使用するためのファイルを準備する必要があります。 フォントのドライバーが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556259" data-raw-source="[&lt;strong&gt;DrvQueryAdvanceWidths&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556259)"><strong>DrvQueryAdvanceWidths</strong></a></p></td>
<td align="left"><p>指定された一連のグリフの GDI 文字アドバンス幅を送信するドライバーを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556263" data-raw-source="[&lt;strong&gt;DrvQueryFontCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556263)"><strong>DrvQueryFontCaps</strong></a></p></td>
<td align="left"><p>指定されたバッファーにフォント ドライバーの機能を定義するビットの配列にコピーします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556265" data-raw-source="[&lt;strong&gt;DrvQueryFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556265)"><strong>DrvQueryFontFile</strong></a></p></td>
<td align="left"><p>クエリのモードによっては、フォント ファイル、またはわかりやすい文字列にフォント フェイスの数を返します。 フォントのドライバーが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556267" data-raw-source="[&lt;strong&gt;DrvQueryGlyphAttrs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556267)"><strong>DrvQueryGlyphAttrs</strong></a></p></td>
<td align="left"><p>フォントのグリフについての情報を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557287" data-raw-source="[&lt;strong&gt;DrvUnloadFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557287)"><strong>DrvUnloadFontFile</strong></a></p></td>
<td align="left"><p>ドライバーが必要なクリーンアップを行うために、フォント ファイルが必要がなくなったらドライバーに通知します。 フォントのドライバーが必要です。</p></td>
</tr>
</tbody>
</table>

 

GDI の呼び出し、 *DrvLoadFontFile*フォントの実現を作成するために使用する特定のファイルで関数をします。 この関数は、フォント ドライバーののみ必要です。 ときに、関数*DrvLoadFontFile*が呼び出されると、ドライバーは、ファイルを使用するための準備に必要な変換を実行します。

*DrvLoadFontFile* GDI フォントの GDI で維持される使用量のテーブルを使用して、適切なフォントを要求することができる一意の識別子を返します。 フォントが読み込まれると、GDI が再度読み込まれるのと同じフォントは呼び出しません。

GDI 呼び出し*DrvUnloadFontFile*ときに、指定したフォント ファイルは不要です。 *DrvUnloadFontFile*関数は、フォント ドライバーにのみ必要です。 *DrvUnloadFontFile*すべてスクラッチ ファイルが削除され、割り当てられているすべてのシステム リソースが解放されます。

GDI の呼び出し、 *DrvQueryFontFile*ドライバーが読み込まれているフォント ファイルに関する情報を返す関数。 *DrvQueryFontFile*フォント ドライバーにのみ必要です。 によって返される情報の種類が指定された*i モード*します。 場合*i モード*は QFF\_説明、関数は、文字列を返します、フォント ファイルを記述する Microsoft NT ベースのオペレーティング システムの使用します。 場合*i モード*は QFF\_NUMFACES、関数で、フォント ファイルでの顔の数が返されます。 面は、インデックス 1 の範囲から顔の数によって識別されます。

 

 





