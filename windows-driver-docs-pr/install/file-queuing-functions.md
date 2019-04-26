---
title: ファイルのキュー関数
description: ファイルのキュー関数
ms.assetid: ad777cd9-99ca-4468-b1fa-608503f96cd4
keywords:
- SetupAPI 関数 WDK、ファイル、キュー
- キューの WDK SetupAPI ファイルします。
- キューに WDK SetupAPI ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd0abb08b262aec7ab0780198259a6c2b1ee1546
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352082"
---
# <a name="file-queuing-functions"></a>ファイルのキュー関数





一般的なセットアップ機能を使用して、ファイルのさまざまな操作をキューできます。 ファイルのキューは、コピー、名前の変更、およびファイルの削除を確立できます。 通常、アプリケーション全体のインストールに必要なすべてのファイル操作をキューし、「コミット」キュー 1 つのバッチで行われるようにします。

次の表では、ファイルのキュー関数の概要を示します。 関数の詳細な説明については、Microsoft Windows SDK のドキュメントを参照してください。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376984" data-raw-source="[&lt;strong&gt;SetupCloseFileQueue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376984)"><strong>SetupCloseFileQueue</strong></a></p></td>
<td align="left"><p>任意のコミットされていないファイルの操作と共にファイル キューが破棄されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376987" data-raw-source="[&lt;strong&gt;SetupCommitFileQueue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376987)"><strong>SetupCommitFileQueue</strong></a></p></td>
<td align="left"><p>コミット (を実行する) すべての操作がキューに登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377408" data-raw-source="[&lt;strong&gt;SetupOpenFileQueue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377408)"><strong>SetupOpenFileQueue</strong></a></p></td>
<td align="left"><p>作成し、ファイルのキューへのハンドルを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377413" data-raw-source="[&lt;strong&gt;SetupPromptReboot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377413)"><strong>SetupPromptReboot</strong></a></p></td>
<td align="left"><p>必要な場合は、ユーザーに自分のコンピューターの再起動を求められます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377421" data-raw-source="[&lt;strong&gt;SetupQueueCopy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377421)"><strong>SetupQueueCopy</strong></a></p></td>
<td align="left"><p>指定されたファイルをコピーするためキューに入れます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377422" data-raw-source="[&lt;strong&gt;SetupQueueCopyIndirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377422)"><strong>SetupQueueCopyIndirect</strong></a></p></td>
<td align="left"><p>キューにコピーするには、指定したファイルとファイルの場所とセキュリティ情報を提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377423" data-raw-source="[&lt;strong&gt;SetupQueueCopySection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377423)"><strong>SetupQueueCopySection</strong></a></p></td>
<td align="left"><p>キューで指定した INF ファイルはファイルをコピーするためのセクションです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377424" data-raw-source="[&lt;strong&gt;SetupQueueDefaultCopy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377424)"><strong>SetupQueueDefaultCopy</strong></a></p></td>
<td align="left"><p>指定されたファイルをコピーするために INF ファイルに含まれている、既定の元とコピー先の設定を使用してキューを配置します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377425" data-raw-source="[&lt;strong&gt;SetupQueueDelete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377425)"><strong>SetupQueueDelete</strong></a></p></td>
<td align="left"><p>指定されたファイルの削除をキューします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377426" data-raw-source="[&lt;strong&gt;SetupQueueDeleteSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377426)"><strong>SetupQueueDeleteSection</strong></a></p></td>
<td align="left"><p>キュー、INF 内のファイルはファイル削除のセクションです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377427" data-raw-source="[&lt;strong&gt;SetupQueueRename&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377427)"><strong>SetupQueueRename</strong></a></p></td>
<td align="left"><p>指定されたファイルの名前を変更するキューに入れます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377428" data-raw-source="[&lt;strong&gt;SetupQueueRenameSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377428)"><strong>SetupQueueRenameSection</strong></a></p></td>
<td align="left"><p>キューの名前変更、INF セクションではファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377435" data-raw-source="[&lt;strong&gt;SetupScanFileQueue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377435)"><strong>SetupScanFileQueue</strong></a></p></td>
<td align="left"><p>ファイルのキューを走査し、キューのエントリごとに指定された操作を実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377440" data-raw-source="[&lt;strong&gt;SetupSetPlatformPathOverride&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377440)"><strong>SetupSetPlatformPathOverride</strong></a></p></td>
<td align="left"><p>既定のプラットフォーム固有のソース パスをオーバーライドするために使用される値を設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





