---
title: オプションのグラフィックス ドライバー関数
description: オプションのグラフィックス ドライバー関数
ms.assetid: 3cdef152-4bcc-426a-9aa7-fd94acf2331f
keywords:
- GDI WDK Windows 2000 の表示、関数、省略可能
- グラフィック ドライバー WDK Windows 2000 の表示、機能、省略可能
- WDK のグラフィックス、省略可能な関数
- WDK GDI、関数、省略可能な描画
- GDI WDK Windows 2000 の表示、DDI、省略可能な関数
- グラフィックス ドライバー WDK Windows 2000 の表示、DDI、省略可能な関数
- DDI WDK グラフィックス、省略可能な関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410e473c099320d35ac371e7e5fa9f564bba6ac1
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349411"
---
# <a name="optional-graphics-driver-functions"></a>オプションのグラフィックス ドライバー関数


## <span id="ddk_optional_graphics_driver_functions_gg"></span><span id="DDK_OPTIONAL_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


ドライバーのサイズを小さくの関心事、ドライバー開発者は、通常はハードウェアで適切にサポートされている省略可能な関数だけを追加します。 たとえば、Image Color Management (ICM) をサポートするハードウェアのドライバーを実装、 *DrvIcmXxx*関数。 次の表には、グラフィック ドライバーを実装できます必要に応じて関数が一覧表示します。

### <a name="span-iddisplayandprinterdriverfunctionsspanspan-iddisplayandprinterdriverfunctionsspanspan-iddisplayandprinterdriverfunctionsspandisplay-and-printer-driver-functions"></a><span id="Display_and_Printer_Driver_Functions_"></span><span id="display_and_printer_driver_functions_"></span><span id="DISPLAY_AND_PRINTER_DRIVER_FUNCTIONS_"></span>画面およびプリンター ドライバーの機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ ポイント</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556176" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556176)"><strong>DrvAlphaBlend</strong></a></p></td>
<td align="left"><p>ビット ブロック転送機能を提供します<a href="https://msdn.microsoft.com/library/windows/hardware/ff556270#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"><em>アルファ ブレンド</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556180" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556180)"><strong>DrvBitBlt</strong></a></p></td>
<td align="left"><p>サーフェスからの一般的なビット ブロック転送を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556185" data-raw-source="[&lt;strong&gt;DrvCreateDeviceBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556185)"><strong>DrvCreateDeviceBitmap</strong></a></p></td>
<td align="left"><p>作成し、ドライバーの定義済みの形式のビットマップを管理します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556187" data-raw-source="[&lt;strong&gt;DrvDeleteDeviceBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556187)"><strong>DrvDeleteDeviceBitmap</strong></a></p></td>
<td align="left"><p>デバイス管理のビットマップを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556202" data-raw-source="[&lt;strong&gt;DrvDitherColor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556202)"><strong>DrvDitherColor</strong></a></p></td>
<td align="left"><p>要求に対しては、ブラシの作成、デバイス、ディザリングを<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-palette" data-raw-source="&lt;em&gt;device palette&lt;/em&gt;"><em>デバイス パレット</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556220" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556220)"><strong>DrvFillPath</strong></a></p></td>
<td align="left"><p>閉じたパスを描画、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surface&lt;/em&gt;"><em>画面のデバイスで管理された</em></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556236" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556236)"><strong>DrvGradientFill</strong></a></p></td>
<td align="left"><p>指定したプリミティブ網掛けを適用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556238" data-raw-source="[&lt;strong&gt;DrvIcmCheckBitmapBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556238)"><strong>DrvIcmCheckBitmapBits</strong></a></p></td>
<td align="left"><p>指定したビットマップのピクセルが、指定した変換のデバイスの色域内にあるかどうかを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556239" data-raw-source="[&lt;strong&gt;DrvIcmCreateColorTransform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556239)"><strong>DrvIcmCreateColorTransform</strong></a></p></td>
<td align="left"><p>ICM の色変換を作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556241" data-raw-source="[&lt;strong&gt;DrvIcmDeleteColorTransform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556241)"><strong>DrvIcmDeleteColorTransform</strong></a></p></td>
<td align="left"><p>指定した ICM 色変換を削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556243" data-raw-source="[&lt;strong&gt;DrvIcmSetDeviceGammaRamp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556243)"><strong>DrvIcmSetDeviceGammaRamp</strong></a></p></td>
<td align="left"><p>ハードウェアの設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff556283#wdkgloss-gamma-ramp" data-raw-source="&lt;em&gt;gamma ramp&lt;/em&gt;"><em>ガンマごとの傾斜増加</em></a>の指定した表示デバイス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556245" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556245)"><strong>DrvLineTo</strong></a></p></td>
<td align="left"><p>1 つの整数のみ表面的な実線を描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556258" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556258)"><strong>DrvPlgBlt</strong></a></p></td>
<td align="left"><p>回転のビット ブロック転送サーフェス デバイス管理し、GDI 管理の組み合わせ間での機能を提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556273" data-raw-source="[&lt;strong&gt;DrvRealizeBrush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556273)"><strong>DrvRealizeBrush</strong></a></p></td>
<td align="left"><p>定義されたサーフェイスでの指定したブラシに気付きます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556302" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556302)"><strong>DrvStretchBlt</strong></a></p></td>
<td align="left"><p>デバイス管理し、GDI 管理画面間でのブロックの転送を拡大できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556306" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556306)"><strong>DrvStretchBltROP</strong></a></p></td>
<td align="left"><p>使用して伸縮ビット ブロック転送を実行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff556331#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"> <em>ROP</em></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556311" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556311)"><strong>DrvStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>同時に入力され、パスの輪郭を描きます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556323" data-raw-source="[&lt;strong&gt;DrvSynchronize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556323)"><strong>DrvSynchronize</strong></a></p></td>
<td align="left"><p>GDI とディスプレイのコプロセッサのドライバーでサポートされているデバイスの間の描画操作の座標<a href="https://msdn.microsoft.com/library/windows/hardware/ff556279#wdkgloss-engine-managed-surface" data-raw-source="&lt;em&gt;engine-managed surfaces&lt;/em&gt;"><em>サーフェスのエンジン管理</em></a>のみです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557273" data-raw-source="[&lt;strong&gt;DrvSynchronizeSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557273)"><strong>DrvSynchronizeSurface</strong></a></p></td>
<td align="left"><p>GDI とディスプレイのコプロセッサのドライバーでサポートされているデバイスの間の描画操作の座標エンジンに管理されたサーフェイスのみです。 ドライバーは、両方を提供する場合<em>DrvSynchronize</em>と<em>DrvSynchronizeSurface</em>、GDI はのみ呼び出す<em>DrvSynchronizeSurface</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557283" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557283)"><strong>DrvTransparentBlt</strong></a></p></td>
<td align="left"><p>透過性のビット ブロック転送機能を提供します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctionsusedexclusivelybydisplaydriversspanspan-idfunctionsusedexclusivelybydisplaydriversspanspan-idfunctionsusedexclusivelybydisplaydriversspanfunctions-used-exclusively-by-display-drivers"></a><span id="Functions_Used_Exclusively_by_Display_Drivers"></span><span id="functions_used_exclusively_by_display_drivers"></span><span id="FUNCTIONS_USED_EXCLUSIVELY_BY_DISPLAY_DRIVERS"></span>ディスプレイ ドライバーによって排他的に使用する関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ ポイント</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556248" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556248)"><strong>DrvMovePointer</strong></a></p></td>
<td align="left"><p>新しい位置にポインターを移動し、再描画します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556278" data-raw-source="[&lt;strong&gt;DrvSaveScreenBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556278)"><strong>DrvSaveScreenBits</strong></a></p></td>
<td align="left"><p>保存または画面 (ディスプレイ ドライバーのみ) の指定した四角形を復元します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556289" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556289)"><strong>DrvSetPointerShape</strong></a></p></td>
<td align="left"><p>ドライバーが引かれて、新しいポインターの形を設定し、場合に、ポインターの画面から削除します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctionsusedprimarilybyprinterdriversspanspan-idfunctionsusedprimarilybyprinterdriversspanspan-idfunctionsusedprimarilybyprinterdriversspanfunctions-used-primarily-by-printer-drivers"></a><span id="Functions_Used_Primarily_by_Printer_Drivers"></span><span id="functions_used_primarily_by_printer_drivers"></span><span id="FUNCTIONS_USED_PRIMARILY_BY_PRINTER_DRIVERS"></span>プリンター ドライバーで主に使用される関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ ポイント</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556192" data-raw-source="[&lt;strong&gt;DrvDestroyFont&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556192)"><strong>DrvDestroyFont</strong></a></p></td>
<td align="left"><p>ドライバーに通知するフォントの実現化が不要になった。ドライバーは、割り当て済みのデータ構造体を解放できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556203" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556203)"><strong>DrvDrawEscape</strong></a></p></td>
<td align="left"><p>描画型エスケープ関数を実装します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556217" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556217)"><strong>DrvEscape</strong></a></p></td>
<td align="left"><p>デバイスに依存しない DDI では使用できないデバイスからの情報を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556226" data-raw-source="[&lt;strong&gt;DrvFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556226)"><strong>DrvFree</strong></a></p></td>
<td align="left"><p>指定されたデータ構造体に関連付けられているフォントの記憶域を解放します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfunctionsusedexclusivelybyprinterdriversspanspan-idfunctionsusedexclusivelybyprinterdriversspanspan-idfunctionsusedexclusivelybyprinterdriversspanfunctions-used-exclusively-by-printer-drivers"></a><span id="Functions_Used_Exclusively_by_Printer_Drivers"></span><span id="functions_used_exclusively_by_printer_drivers"></span><span id="FUNCTIONS_USED_EXCLUSIVELY_BY_PRINTER_DRIVERS"></span>プリンター ドライバーによって排他的に使用する関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ ポイント</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556215" data-raw-source="[&lt;strong&gt;DrvEndDoc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556215)"><strong>DrvEndDoc</strong></a></p></td>
<td align="left"><p>ドキュメントの情報を送信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556223" data-raw-source="[&lt;strong&gt;DrvFontManagement&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556223)"><strong>DrvFontManagement</strong></a></p></td>
<td align="left"><p>GDI を介して直接使用できるプリンターの機能にアクセスをできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556230" data-raw-source="[&lt;strong&gt;DrvGetGlyphMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556230)"><strong>DrvGetGlyphMode</strong></a></p></td>
<td align="left"><p>特定のフォント、フォント情報の種類を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556250" data-raw-source="[&lt;strong&gt;DrvNextBand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556250)"><strong>DrvNextBand</strong></a></p></td>
<td align="left"><p>画面のだけ描画バンドの内容を認識しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556268" data-raw-source="[&lt;em&gt;DrvQueryPerBandInfo&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556268)"><em>DrvQueryPerBandInfo</em></a></p></td>
<td align="left"><p>バンドの縞模様プリンターを指定した画面の情報を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556281" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556281)"><em>DrvSendPage</em></a></p></td>
<td align="left"><p>生のビットを画面からプリンターに送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556292" data-raw-source="[&lt;strong&gt;DrvStartBanding&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556292)"><strong>DrvStartBanding</strong></a></p></td>
<td align="left"><p>縞模様のドライバーを準備します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556296" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556296)"><strong>DrvStartDoc</strong></a></p></td>
<td align="left"><p>コントロールの開始ドキュメントの情報を送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556298" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556298)"><strong>DrvStartPage</strong></a></p></td>
<td align="left"><p>コントロールの開始とページの情報を送信します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfontdriverfunctionspanspan-idfontdriverfunctionspanspan-idfontdriverfunctionspanfont-driver-function"></a><span id="Font_Driver_Function"></span><span id="font_driver_function"></span><span id="FONT_DRIVER_FUNCTION"></span>フォント ドライバー関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エントリ ポイント</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556259" data-raw-source="[&lt;strong&gt;DrvQueryAdvanceWidths&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556259)"><strong>DrvQueryAdvanceWidths</strong></a></p></td>
<td align="left"><p>指定された一連のグリフのアドバンス幅を文字を提供します。</p></td>
</tr>
</tbody>
</table>

 

 

 





