---
title: 条件的に必須のグラフィックス ドライバー関数
description: 条件的に必須のグラフィックス ドライバー関数
ms.assetid: db5816e2-83a1-491d-99f5-d693fefcf1fd
keywords:
- GDI WDK Windows 2000 の表示、関数、条件付きで必要です。
- グラフィック ドライバー WDK Windows 2000 を表示するために必要な条件付きで関数
- WDK のグラフィックス、条件付きで必要なときに、関数
- WDK の GDI、関数、条件付きで必要な描画
- GDI WDK Windows 2000 の表示、DDI、条件付きで必須の関数
- グラフィックス ドライバー WDK Windows 2000 表示、DDI、条件付きで必要な関数
- DDI WDK グラフィックス、条件付きで必要な関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cca1fcf72c7d18e8658557ea9bd498de08f35d9
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349189"
---
# <a name="conditionally-required-graphics-driver-functions"></a>条件的に必須のグラフィックス ドライバー関数


## <span id="ddk_conditionally_required_graphics_driver_functions_gg"></span><span id="DDK_CONDITIONALLY_REQUIRED_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


この関数は、常に必要なだけでなく他の特定の関数が、ドライバーの実装方法によって、必要な可能性があります。 条件付きで必要な関数は、次の表に表示されます。 ドライバーが、独自のプライマリ画面を管理する場合 (を使用して、 **EngCreateDeviceSurface**通常これらの操作のほとんどまたはすべてを管理する GDI を許可します。 設定可能なパレットをサポートする表示をサポートする必要がありますも、 [ **DrvSetPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff556282)関数。

フォントの描画を定義またはディスプレイ ドライバーよりもプリンター ドライバーの方が一般的です。 ディスプレイ ドライバーは、フォントを処理する必要はありません。 ハードウェアに常駐しているフォントがある場合は、ドライバーは GDI フォントについての情報を指定する必要があります。 この情報には、フォント メトリック、Unicode から個々 のグリフの id、個々 のグリフの属性、およびカーニング テーブルへのマッピングが含まれています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ ポイント</th>
<th align="left">必要な場合</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556182" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556182)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;Device-managed surfaces&lt;/em&gt;"><em>デバイス管理の画面</em></a></p></td>
<td align="left"><p>デバイスで管理されたラスター サーフェスと GDI 標準形式のビットマップを変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556190" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556190)"><strong>DrvDescribePixelFormat</strong></a></p></td>
<td align="left"><p>1 つの画面上の別のピクセル形式の windows をサポートする表示します</p></td>
<td align="left"><p>PDEV のピクセル形式をについて説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556235" data-raw-source="[&lt;strong&gt;DrvGetTrueTypeFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556235)"><strong>DrvGetTrueTypeFile</strong></a></p></td>
<td align="left"><p>TrueType フォント ドライバー</p></td>
<td align="left"><p>TrueType フォント メモリ マップト ファイルに、GDI にアクセスします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556247" data-raw-source="[&lt;strong&gt;DrvLoadFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556247)"><strong>DrvLoadFontFile</strong></a></p></td>
<td align="left"><p>フォント ドライバー</p></td>
<td align="left"><p>フォントの実現に使用するファイルを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556262" data-raw-source="[&lt;strong&gt;DrvQueryFont&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556262)"><strong>DrvQueryFont</strong></a></p></td>
<td align="left"><p>プリンター ドライバー</p></td>
<td align="left"><p>特定のフォントの GDI 構造体を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556263" data-raw-source="[&lt;strong&gt;DrvQueryFontCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556263)"><strong>DrvQueryFontCaps</strong></a></p></td>
<td align="left"><p>フォント ドライバー</p></td>
<td align="left"><p>フォント ドライバーの機能のドライバーを要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556264" data-raw-source="[&lt;strong&gt;DrvQueryFontData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556264)"><strong>DrvQueryFontData</strong></a></p></td>
<td align="left"><p>プリンター ドライバー</p></td>
<td align="left"><p>実現されたフォントに関する情報を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556265" data-raw-source="[&lt;strong&gt;DrvQueryFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556265)"><strong>DrvQueryFontFile</strong></a></p></td>
<td align="left"><p>フォント ドライバー</p></td>
<td align="left"><p>ドライバーのフォント ファイルの情報を要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556266" data-raw-source="[&lt;strong&gt;DrvQueryFontTree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556266)"><strong>DrvQueryFontTree</strong></a></p></td>
<td align="left"><p>プリンター ドライバー</p></td>
<td align="left"><p>次の 3 つの種類のフォントのマッピングのいずれかを定義するツリー構造を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556269" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeOutline&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556269)"><strong>DrvQueryTrueTypeOutline</strong></a></p></td>
<td align="left"><p>TrueType フォント ドライバー</p></td>
<td align="left"><p>GDI に truetype フォントのグリフのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556271" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556271)"><strong>DrvQueryTrueTypeTable</strong></a></p></td>
<td align="left"><p>TrueType フォント ドライバー</p></td>
<td align="left"><p>TrueType フォント ファイルに、GDI にアクセスします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556276" data-raw-source="[&lt;strong&gt;DrvResetPDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556276)"><strong>DrvResetPDEV</strong></a></p></td>
<td align="left"><p>ドキュメント モードの変更を許可するデバイス</p></td>
<td align="left"><p>新しい PDEV に古い PDEV からドライバーの状態を転送します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556282" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556282)"><strong>DrvSetPalette</strong></a></p></td>
<td align="left"><p>設定可能なパレットをサポートする表示します</p></td>
<td align="left"><p>指定したデバイスのパレットに気付きます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556285" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556285)"><strong>DrvSetPixelFormat</strong></a></p></td>
<td align="left"><p>1 つの画面上の別のピクセル形式の windows をサポートする表示します</p></td>
<td align="left"><p>ウィンドウのピクセル形式を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556316" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556316)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p>デバイス管理の画面</p></td>
<td align="left"><p>ディスプレイ上のパスを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556322" data-raw-source="[&lt;strong&gt;DrvSwapBuffers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556322)"><strong>DrvSwapBuffers</strong></a></p></td>
<td align="left"><p>ダブル バッファリングのピクセル形式をサポートするドライバー</p></td>
<td align="left"><p>画面の非表示のバッファーの内容を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557277" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557277)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p>デバイス管理のサーフェスまたはドライバーのフォントを定義します。</p></td>
<td align="left"><p>指定した位置にある文字のイメージ (グリフ) のセットを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557287" data-raw-source="[&lt;strong&gt;DrvUnloadFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557287)"><strong>DrvUnloadFontFile</strong></a></p></td>
<td align="left"><p>フォント ドライバー</p></td>
<td align="left"><p>フォント ファイルは必要ないことをドライバーに通知します。</p></td>
</tr>
</tbody>
</table>

 

 

 





