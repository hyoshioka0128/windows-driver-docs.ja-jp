---
title: プリンター構成コマンド
description: プリンター構成コマンド
ms.assetid: ed5102e7-1651-4188-8042-f0d544a54a1d
keywords:
- プリンター コマンド WDK Unidrv、構成
- 構成コマンド WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab87b04eac3c5bbfce2bdd4c481c5e3e2461972
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380529"
---
# <a name="printer-configuration-commands"></a>プリンター構成コマンド





次の表は、プリンターの構成コマンドを一覧表示します。 すべてのコマンドを指定する、[コマンド エントリ形式](command-entry-format.md)します。

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
<td><p>CmdStartJob</p></td>
<td><p>印刷ジョブを初期化するためにコマンド。</p></td>
<td><p>任意。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">コマンドの実行順序</a>指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>CmdStartDoc</p></td>
<td><p>ドキュメントを初期化するためにコマンド。</p></td>
<td><p>任意。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">コマンドの実行順序</a>指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>CmdStartPage</p></td>
<td><p>ページを初期化し、カーソルの座標を (0, 0) のカーソル位置を設定するコマンドです。</p></td>
<td><p>任意。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">コマンドの実行順序</a>指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndPage</p></td>
<td><p>ページの印刷が完了するコマンドです。</p></td>
<td><p>任意。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">コマンドの実行順序</a>指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEndDoc</p></td>
<td><p>ドキュメントの印刷を終了するコマンドです。</p></td>
<td><p>任意。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">コマンドの実行順序</a>指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndJob</p></td>
<td><p>印刷ジョブを完了するコマンドです。</p></td>
<td><p>任意。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">コマンドの実行順序</a>指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>CmdCopies</p></td>
<td><p>印刷するコピーの数を指定するコマンドです。</p></td>
<td><p>任意。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">コマンドの実行順序</a>指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>CmdSleepTimeOut</p></td>
<td><p>プリンターが省電力モードに入る前に待機する時間 (分) の数を指定するコマンド。</p></td>
<td><p>任意。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">コマンドの実行順序</a>指定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




