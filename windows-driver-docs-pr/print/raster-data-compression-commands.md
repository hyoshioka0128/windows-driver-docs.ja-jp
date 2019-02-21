---
title: ラスター データ圧縮コマンド
description: ラスター データ圧縮コマンド
ms.assetid: fd88d009-7612-49cc-810a-b0d09b4b75b3
keywords:
- データ圧縮のラスター印刷コマンド WDK Unidrv
- 圧縮ラスター印刷コマンド WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61d0cbd6e83971a660d1371d89295be0d11ae66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531131"
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
<td><p>プリンターを無効にするコマンド&#39;s 受け入れのすべての圧縮されたデータ型。</p></td>
<td><p>(省略可能)。</p></td>
</tr>
<tr class="even">
<td><p>CmdEnableDRC</p></td>
<td><p>プリンターを有効にするコマンド&#39;s 民主共和国で圧縮されたデータに同意します。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv はデルタ行の圧縮を使用しません。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEnableFE_RLE</p></td>
<td><p>プリンターを有効にするコマンド&#39;s FE RLE 圧縮されたデータに同意します。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv は FE RLE 圧縮を使用しません。</p></td>
</tr>
<tr class="even">
<td><p>CmdEnableOEMComp</p></td>
<td><p>プリンターを有効にするコマンド&#39;カスタマイズされた圧縮データ型の %s への同意。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv はカスタマイズされたデータの圧縮を使用しません。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEnableTIFF4</p></td>
<td><p>プリンターを有効にするコマンド&#39;s TIFF 4.0 で圧縮されたデータに同意します。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv は TIFF4.0 圧縮を使用しません。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




