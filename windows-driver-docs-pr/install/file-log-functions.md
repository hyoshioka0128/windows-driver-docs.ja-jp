---
title: ファイル ログ関数
description: ファイル ログ関数
ms.assetid: 7d9fe4c9-834f-4dcc-a216-dc6a98ee2fd3
keywords:
- SetupAPI 関数 WDK、ログ ファイル
- ログ ファイル WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 675e7593dbd47703b7881ca9320bf4aea8f7d7bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549698"
---
# <a name="file-log-functions"></a>ファイル ログ関数





ログ ファイルを使用すると、インストール中にシステムにコピーされたファイルに関する情報を記録します。 ログ ファイルには、システム ログまたは独自のインストール ログ ファイルのいずれかを指定できます。

次の表には、ログ ファイルを操作するために使用できる関数が一覧表示します。 関数の説明の詳細については、、 [Microsoft Windows SDK ドキュメント](https://go.microsoft.com/fwlink/p/?linkid=131248)を参照してください。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377397" data-raw-source="[&lt;strong&gt;SetupInitializeFileLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377397)"><strong>SetupInitializeFileLog</strong></a></p></td>
<td align="left"><p>使用するためのログ ファイルを初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377405" data-raw-source="[&lt;strong&gt;SetupLogError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377405)"><strong>SetupLogError</strong></a></p></td>
<td align="left"><p>エラー メッセージをログ ファイルに書き込みます。 (それ使用してください、オペレーティング システムのインストール時にのみ。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377406" data-raw-source="[&lt;strong&gt;SetupLogFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377406)"><strong>SetupLogFile</strong></a></p></td>
<td align="left"><p>ログ ファイルにエントリを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377415" data-raw-source="[&lt;strong&gt;SetupQueryFileLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377415)"><strong>SetupQueryFileLog</strong></a></p></td>
<td align="left"><p>ログ ファイルから情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377429" data-raw-source="[&lt;strong&gt;SetupRemoveFileLogEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377429)"><strong>SetupRemoveFileLogEntry</strong></a></p></td>
<td align="left"><p>ログ ファイルからエントリを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377443" data-raw-source="[&lt;strong&gt;SetupTerminateFileLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377443)"><strong>SetupTerminateFileLog</strong></a></p></td>
<td align="left"><p>ログ ファイルに割り当てられたリソースを解放します。</p></td>
</tr>
</tbody>
</table>

 

 

 





