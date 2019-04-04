---
title: ダウンロードしたフォントのコマンド
description: ダウンロードしたフォントのコマンド
ms.assetid: 5cf6b2bd-5378-4e90-8959-ced978dee02f
keywords:
- ダウンロードしたフォント コマンド WDK Unidrv
- フォントの WDK Unidrv コマンドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02ef483447c5f1a802b09867f46930ae4d332c76
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349399"
---
# <a name="commands-for-downloaded-fonts"></a>ダウンロードしたフォントのコマンド





次の表は、ダウンロードしたフォントを制御するためのコマンドを一覧表示します。 すべてのコマンドを指定する、[コマンド エントリ形式](command-entry-format.md)します。

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
<td><p><strong>CmdDeleteFont</strong></p></td>
<td><p>その識別子を指定してソフト フォントを削除するコマンド。</p></td>
<td><p>任意。 削除されたフォントの割り当てられたメモリをすぐに再利用できる場合にのみ、このコマンドを指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdDeselectFontID</strong></p></td>
<td><p>フォントを非アクティブにするには、現在のフォント ID の選択を解除するコマンド。</p></td>
<td><p>任意。 存在しない場合、現在のフォントが新しいフォントが選択されている場合に選択を解除する必要はありません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectFontHeight</strong></p></td>
<td><p>ダウンロードしたフォントの高さを選択するコマンドです。</p></td>
<td><p>任意。 存在しない場合、プリンターは、スケーラブルでダウンロード可能な実際の型のアウトライン フォントをサポートしていません。 このコマンドは、HPPCL_OUTLINE 形式に必要です。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectFontID</strong></p></td>
<td><p>フォントをアクティブにするには、現在のフォント ID を選択するコマンドです。</p></td>
<td><p>ダウンロードしたフォントをプリンターがサポートしているかが必要です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectFontWidth</strong></p></td>
<td><p>ダウンロードしたフォントの幅を選択するコマンドです。</p></td>
<td><p>任意。 かどうか、存在していないダウンロードのフォントの幅は縦横比の高さ。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetCharCode</strong></p></td>
<td><p>ダウンロードまたは削除するには、次の文字の文字のコードを指定するコマンドです。</p></td>
<td><p>ダウンロードしたフォントをプリンターがサポートしているかが必要です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetFontID</strong></p></td>
<td><p>現在のフォントの ID を設定するコマンド</p></td>
<td><p>ダウンロードしたフォントをプリンターがサポートしているかが必要です。</p></td>
</tr>
</tbody>
</table>

 

例については、、[サンプル GPD ファイル](sample-gpd-files.md)を参照してください。

 

 




