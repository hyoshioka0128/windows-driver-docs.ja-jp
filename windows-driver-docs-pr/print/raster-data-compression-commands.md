---
title: ラスター データ圧縮コマンド
description: ラスター データ圧縮コマンド
ms.assetid: fd88d009-7612-49cc-810a-b0d09b4b75b3
keywords:
- データ圧縮のラスター印刷コマンド WDK Unidrv
- 圧縮ラスター印刷コマンド WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec81fd9a1bb413cbc642c59b0464c4e9ec358c7f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349953"
---
# <a name="raster-data-compression-commands"></a>ラスター データ圧縮コマンド





次の表には、ラスター データの圧縮コマンドが表示されます。 すべてのコマンドを指定する、[コマンド エントリ形式](command-entry-format.md)します。

ラスター データ圧縮コマンドの詳細については、次を参照してください。[ラスター データの圧縮](compressing-raster-data.md)します。

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
<td><p>CmdDisableCompression</p></td>
<td><p>プリンターのすべての圧縮されたデータ型への同意を無効にするコマンドです。</p></td>
<td><p>任意。</p></td>
</tr>
<tr class="even">
<td><p>CmdEnableDRC</p></td>
<td><p>民主共和国で圧縮されたデータのプリンターの受け入れを有効にするコマンドします。</p></td>
<td><p>任意。 指定しない場合、Unidrv はデルタ行の圧縮を使用しません。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEnableFE_RLE</p></td>
<td><p>FE RLE 圧縮データのプリンターの受け入れを有効にするコマンドします。</p></td>
<td><p>任意。 指定しない場合、Unidrv は FE RLE 圧縮を使用しません。</p></td>
</tr>
<tr class="even">
<td><p>CmdEnableOEMComp</p></td>
<td><p>カスタマイズされた圧縮データ型のプリンターの受け入れを有効にするコマンドします。</p></td>
<td><p>任意。 指定しない場合、Unidrv はカスタマイズされたデータの圧縮を使用しません。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEnableTIFF4</p></td>
<td><p>TIFF 4.0 で圧縮されたデータのプリンターの受け入れを有効にするコマンドします。</p></td>
<td><p>任意。 指定しない場合、Unidrv は TIFF4.0 圧縮を使用しません。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




