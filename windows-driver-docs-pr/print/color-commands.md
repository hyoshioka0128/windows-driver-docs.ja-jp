---
title: 色コマンド
description: 色コマンド
ms.assetid: 752a3c1d-05f1-4f5e-9ef2-e51721ef7cc4
keywords:
- プリンターが WDK Unidrv、色をコマンドします。
- 色の WDK Unidrv コマンドします。
- 背景の色のオプション WDK Unidrv
- WDK Unidrv パレット
- WDK Unidrv がパターンします。
- WDK Unidrv ブラシします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 233234cd9a43ad51d98479ddbe4a7e18e7621eac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351938"
---
# <a name="color-commands"></a>色コマンド





このトピックでは、印刷、色のコマンドを説明し、次のセクションが含まれています。

プライマリの背景色を選択するためのコマンド

プリンターのパレットを制御するためのコマンド

パターンのブラシを選択するためのコマンド

すべてのコマンドを指定する、[コマンド エントリ形式](command-entry-format.md)します。

### <a href="" id="ddk-commands-for-selecting-primary-background-colors-gg"></a>プライマリの背景色を選択するためのコマンド

[プリンター コマンド](printer-commands.md)次の表に平面のカラー プリンター (ドット マトリックス プリンターなど) などのプログラミング可能なカラー パレットをサポートしていないプリンターとパレット (たとえば、初期インク ジェット プリンターで使用されますプリンターの場合)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンド</th>
<th>説明</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>CmdSelectBlackColor</strong></td>
<td><p>黒の背景色を選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="even">
<td><strong>CmdSelectBlueColor</strong></td>
<td><p>青色の背景色を選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="odd">
<td><strong>CmdSelectCyanColor</strong></td>
<td><p>水色の背景色を選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="even">
<td><strong>CmdSelectGreenColor</strong></td>
<td><p>緑の背景色を選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="odd">
<td><strong>CmdSelectMagentaColor</strong></td>
<td><p>マゼンタの背景色を選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectRedColor</strong></p></td>
<td><p>赤の背景色を選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectYellowColor</strong></p></td>
<td><p>黄色の背景色を選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectWhiteColor</strong></p></td>
<td><p>白の背景色を選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

### <a href="" id="ddk-commands-for-controlling-printer-palettes-gg"></a>プリンターのパレットを制御するためのコマンド

[プリンター コマンド](printer-commands.md)ラスター印刷の両方 (テキストとベクトル) のフォア グラウンド印刷用プログラミング可能なパレットをサポートするプリンターで、次の表でを使用します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンド</th>
<th>説明</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CmdBeginPaletteDef</strong></p></td>
<td><p>色パレットの定義を初期化するためにコマンド。</p></td>
<td><p>(省略可能)。 指定しない場合、パレットの定義の初期化は必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdEndPaletteDef</strong></p></td>
<td><p>コマンド パレットの定義を終了します。</p></td>
<td><p>(省略可能)。 指定しない場合、パレットの定義を終了するコマンドは必要ありません。</p>
<p><em>順序属性を指定することができます。 そうでない場合、 <strong></em>順序</strong>属性に関連付けられた、最も最近実行された<a href="option-selection-command.md" data-raw-source="[option selection command](option-selection-command.md)">選択コマンドのオプション</a>返さの機能が使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdBeginPaletteReDef</strong></p></td>
<td><p>色パレットの再定義を初期化するためにコマンド。</p></td>
<td><p>(省略可能)。 指定しない場合、パレットの再定義の初期化は必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdEndPaletteReDef</strong></p></td>
<td><p>パレットの再定義を終了するコマンドです。</p></td>
<td><p>(省略可能)。 指定しない場合、パレットの再定義を終了するコマンドは必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdDefinePaletteEntry</strong></p></td>
<td><p>パレット エントリを定義するコマンドです。</p></td>
<td><p>プリンターがパレットをサポートしているかが必要です。</p>
<p>モードでは 24 BPP、Unidrv は対象のパレットを<em>PaletteSize は 1 です。 これにより、GPD 開発者が自分のデバイスのダイレクト RGB 色の選択コマンドを実装します。 これを行うには、次のように設定します。  <strong></em>PaletteSize</strong>を 1 に選択範囲の色のコマンドを指定し、 <strong>CmdDefinePaletteEntry</strong>コマンド。 CmdSelectPaletteEntry コマンドも指定する必要がありますが、として定義することができます、 <strong>NULL</strong>コマンド。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdRedefinePaletteEntry</strong></p></td>
<td><p>コマンド パレット エントリを再定義します。</p></td>
<td><p>(省略可能)。 指定しない場合、 <strong>CmdDefinePaletteEntry</strong>再定義されたパレット エントリに使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectPaletteEntry</strong></p></td>
<td><p>現在の色とパレット エントリを選択するコマンドです。</p></td>
<td><p>プリンターがパレットをサポートしているかが必要です。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

### <a href="" id="ddk-commands-for-selecting-pattern-brushes-gg"></a>パターンのブラシを選択するためのコマンド

[プリンター コマンド](printer-commands.md)ダウンロードとパターンのブラシの選択をサポートするプリンターで、次の表でを使用します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンド</th>
<th>説明</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CmdDownloadPattern</strong></p></td>
<td><p>プリンターにブラシ パターンを提供するコマンドです。</p></td>
<td><p>(省略可能)。 指定した場合<strong>CmdSelectPattern</strong>も指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectBlackBrush</strong></p></td>
<td><p>現在のブラシとして黒いソリッド ブラシをコマンドします。</p></td>
<td><p>プリンターがブラシをサポートしているかが必要です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectPattern</strong></p></td>
<td><p>ダウンロードしたブラシ パターンを選択するコマンドです。</p></td>
<td><p>(省略可能)。 指定した場合<strong>CmdDownloadPattern</strong>も指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectWhiteBrush</strong></p></td>
<td><p>現在のブラシとして白ソリッド ブラシを選択するコマンドです。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
</tbody>
</table>

 

 

 




