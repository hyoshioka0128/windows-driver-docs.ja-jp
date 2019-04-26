---
title: シミュレーションしたフォントのコマンド
description: シミュレーションしたフォントのコマンド
ms.assetid: 3bfdcf86-35ac-4b95-9efd-31f79a8b9871
keywords:
- シミュレートされたフォントの WDK Unidrv コマンドします。
- フォントの WDK Unidrv コマンドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc65447889349cf1071c4bb64654a005062c146
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355896"
---
# <a name="commands-for-simulated-fonts"></a>シミュレーションしたフォントのコマンド





次の表は、シミュレートされたフォントを制御するためのコマンドを一覧表示します。 すべてのコマンドを指定する、[コマンド エントリ形式](command-entry-format.md)します。

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
<td><p><strong>CmdBoldOff</strong></p></td>
<td><p>太字を無効にするコマンドです。</p></td>
<td><p>(省略可能)。 場合に指定する必要があります<strong>CmdBoldOn</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdBoldOn</strong></p></td>
<td><p>太字を有効にするコマンドです。</p></td>
<td><p>(省略可能)。 Unidrv が太字と送信を有効にするには、このコマンドを送信する場合は、指定された<strong>CmdBoldOff</strong>太字を無効にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdClearAllFontAttribs</strong></p></td>
<td><p>無効にする 1 つのコマンドは、太字、斜体、および下線の機能。</p></td>
<td><p>(省略可能)。 できます、ボールド、プリンターをサポートする斜体、または下線がサポートしているかをすべて無効にする 1 つのコマンドのみに指定します。 代わりに使用<strong>CmdBoldOff</strong>、 <strong>CmdItalicOff</strong>と<strong>CmdUnderlineOff</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdItalicOff</strong></p></td>
<td><p>斜体を無効にするコマンドです。</p></td>
<td><p>(省略可能)。 場合に指定する必要があります<strong>CmdItalicOn</strong>を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdItalicOn</strong></p></td>
<td><p>斜体を有効にするコマンドです。</p></td>
<td><p>(省略可能)。 Unidrv が斜体と送信を有効にするには、このコマンドを送信する場合は、指定された<strong>CmdItalicOff</strong>斜体を無効にします。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectDoubleByteMode</strong></p></td>
<td><p>2 バイトの印刷を有効にするコマンドします。</p></td>
<td><p>(省略可能)。 場合に指定する必要があります<strong>CmdSelectSingleByteMode</strong>を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectSingleByteMode</strong></p></td>
<td><p>1 バイトの印刷を有効にするコマンドします。</p></td>
<td><p>(省略可能)。 必要があります、プリンターが 1 バイトと 2 バイトのモードの間で切り替えることができるかどうかに指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetFontSim</strong></p></td>
<td><p>太字、斜体、下線、1 つのコマンドと取り消し機能。</p></td>
<td><p>(省略可能)。 指定してください (フォントの特性が格納されていないプリンター) のフォントが使用されるたびにする必要がありますのフォント特性に設定するかどうか。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdStrikeThruOff</strong></p></td>
<td><p>取り消し線を無効にするコマンドです。</p></td>
<td><p>(省略可能)。 場合に指定する必要があります<strong>CmdStrikeThruOn</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdStrikeThruOn</strong></p></td>
<td><p>取り消し線を有効にするコマンドします。</p></td>
<td><p>(省略可能)。 指定した場合、Unidrv は取り消し線を有効にするには、このコマンドを送信し、送信<strong>CmdStrikeThruOff</strong>取り消しを無効にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdUnderlineOff</strong></p></td>
<td><p>下線を無効にするコマンドです。</p></td>
<td><p>(省略可能)。 場合に指定する必要があります<strong>CmdUnderlineOn</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdUnderlineOn</strong></p></td>
<td><p>下線が有効にするコマンドです。</p></td>
<td><p>(省略可能)。 Unidrv が下線と送信を有効にするには、このコマンドを送信する場合は、指定された<strong>CmdUnderlineOff</strong>下線を無効にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdVerticalPrintingOff</strong></p></td>
<td><p>垂直方向の印刷を無効にするコマンドです。</p></td>
<td><p>(省略可能)。 場合に指定する必要があります<strong>CmdVerticalPrintingOn</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdVerticalPrintingOn</strong></p></td>
<td><p>垂直方向の印刷を有効にするコマンドです。</p></td>
<td><p>(省略可能)。 必要があります、プリンターが垂直方向の印刷をサポートしているかどうかに指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdWhiteTextOff</strong></p></td>
<td><p>白いテキストの印刷を無効にするコマンドします。</p></td>
<td><p>(省略可能)。 場合に指定する必要があります<strong>CmdWhiteTextOn</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdWhiteTextOn</strong></p></td>
<td><p>白いテキストの印刷を有効にするコマンドします。</p></td>
<td><p>(省略可能)。 指定した場合、Unidrv は白いテキストの印刷を有効にするには、このコマンドを送信し、送信<strong>CmdWhiteTextOff</strong>白いテキストの印刷を無効にします。 (このコマンドは、下位の提供されて GPC 3.0 との互換性。)</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




