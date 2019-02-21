---
title: INF ファイルの処理関数します。
description: INF ファイルの処理関数します。
ms.assetid: df769d05-9843-44d2-971d-13f1a81755c2
keywords:
- SetupAPI 関数 WDK、INF ファイル
- INF ファイル WDK SetupAPI
- SetupCopyOEMInf
- 処理関数 WDK SetupAPI INF ファイル
- 処理関数の WDK INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b0f569074bd759cc377fdfe43528b098a674882
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529418"
---
# <a name="inf-file-processing-functions"></a>INF ファイルの処理関数します。





INF ファイルの処理関数は、次が含まれるセットアップとインストールの機能を提供します。

-   INF ファイルを開いたり閉じたりします。

-   INF ファイルに関する情報を取得しています。

-   ソース ファイルとコピー操作のターゲット ディレクトリに関する情報を取得します。

-   INF ファイルのセクションで指定されたインストールの操作を実行します。

次の表は、INF ファイルを処理するために使用されている関数を一覧表示します。 関数の詳細な説明については、Microsoft Windows SDK のドキュメントを参照してください。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376957" data-raw-source="[&lt;strong&gt;InstallHinfSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376957)"><strong>InstallHinfSection</strong></a></p></td>
<td align="left"><p>指定した INF ファイルで指定されたセクションを実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376985" data-raw-source="[&lt;strong&gt;SetupCloseInfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376985)"><strong>SetupCloseInfFile</strong></a></p></td>
<td align="left"><p>リソースを解放し、INF のハンドルを終了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376990" data-raw-source="[&lt;strong&gt;SetupCopyOEMInf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376990)"><strong>SetupCopyOEMInf</strong></a></p></td>
<td align="left"><p>ファイルをコピー <em>%SystemRoot%\Inf</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376992" data-raw-source="[&lt;strong&gt;SetupDecompressOrCopyFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376992)"><strong>SetupDecompressOrCopyFile</strong></a></p></td>
<td align="left"><p>ファイルをコピーし、必要に応じては、圧縮を解除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376996" data-raw-source="[&lt;strong&gt;SetupFindFirstLine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376996)"><strong>SetupFindFirstLine</strong></a></p></td>
<td align="left"><p>INF ファイルのセクションで、最初の行へのポインターを検索します。 または、キーが指定されている場合、キーと一致する最初の行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376997" data-raw-source="[&lt;strong&gt;SetupFindNextLine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376997)"><strong>SetupFindNextLine</strong></a></p></td>
<td align="left"><p>INF ファイルのセクションでは、次の行にポインターを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377202" data-raw-source="[&lt;strong&gt;SetupFindNextMatchLine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377202)"><strong>SetupFindNextMatchLine</strong></a></p></td>
<td align="left"><p>INF の次の行へのポインターを返すファイルのセクションまたはキーが指定されている場合、次の行をキーと一致します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377254" data-raw-source="[&lt;strong&gt;SetupGetBinaryField&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377254)"><strong>SetupGetBinaryField</strong></a></p></td>
<td align="left"><p>INF ファイル内の指定した行のフィールドからバイナリ データを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377258" data-raw-source="[&lt;strong&gt;SetupGetFieldCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377258)"><strong>SetupGetFieldCount</strong></a></p></td>
<td align="left"><p>行のフィールドの数を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377265" data-raw-source="[&lt;strong&gt;SetupGetFileCompressionInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377265)"><strong>SetupGetFileCompressionInfo</strong></a></p></td>
<td align="left"><p>INF ファイルからファイルの圧縮の情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552194" data-raw-source="[&lt;strong&gt;SetupGetInfDriverStoreLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552194)"><strong>SetupGetInfDriverStoreLocation</strong></a></p></td>
<td align="left"><p>INF ファイルの完全修飾ファイル名 (ディレクトリ パスとファイル名) を取得、<a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">ドライバー ストア</a>システム INF ファイルのディレクトリ内の指定した INF ファイルまたはドライバー ストア内の指定した INF ファイルに対応します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377381" data-raw-source="[&lt;strong&gt;SetupGetInfFileList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377381)"><strong>SetupGetInfFileList</strong></a></p></td>
<td align="left"><p>指定したディレクトリ内には、INF ファイルの一覧を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377383" data-raw-source="[&lt;strong&gt;SetupGetInfInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377383)"><strong>SetupGetInfInformation</strong></a></p></td>
<td align="left"><p>INF ファイルに関する情報を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377385" data-raw-source="[&lt;strong&gt;SetupGetIntField&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377385)"><strong>SetupGetIntField</strong></a></p></td>
<td align="left"><p>INF ファイル内の指定した行で指定されたフィールドの整数値を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552200" data-raw-source="[&lt;strong&gt;SetupGetInfPublishedName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552200)"><strong>SetupGetInfPublishedName</strong></a></p></td>
<td align="left"><p>システム INF ファイルのディレクトリ内の指定した INF ファイルまたはで指定した INF ファイルに対応するシステム INF ファイルのディレクトリの INF ファイルの完全修飾名 (ディレクトリ パスとファイル名) を取得、<a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">ドライバー ストア</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377386" data-raw-source="[&lt;strong&gt;SetupGetLineByIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377386)"><strong>SetupGetLineByIndex</strong></a></p></td>
<td align="left"><p>指定したセクションで指定したインデックス値に関連付けられている行へのポインターを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377387" data-raw-source="[&lt;strong&gt;SetupGetLineCount&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377387)"><strong>SetupGetLineCount</strong></a></p></td>
<td align="left"><p>指定されたセクションには、行の数を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377388" data-raw-source="[&lt;strong&gt;SetupGetLineText&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377388)"><strong>SetupGetLineText</strong></a></p></td>
<td align="left"><p>INF ファイルから特定の行の内容を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377389" data-raw-source="[&lt;strong&gt;SetupGetMultiSzField&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377389)"><strong>SetupGetMultiSzField</strong></a></p></td>
<td align="left"><p>行の指定したフィールドから始まる複数の文字列を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377390" data-raw-source="[&lt;strong&gt;SetupGetSourceFileLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377390)"><strong>SetupGetSourceFileLocation</strong></a></p></td>
<td align="left"><p>INF ファイルに記載されているソース ファイルの場所を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377391" data-raw-source="[&lt;strong&gt;SetupGetSourceFileSize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377391)"><strong>SetupGetSourceFileSize</strong></a></p></td>
<td align="left"><p>指定されたファイルのサイズまたは INF ファイルの指定したセクションに記載されているファイルのセットを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377392" data-raw-source="[&lt;strong&gt;SetupGetSourceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377392)"><strong>SetupGetSourceInfo</strong></a></p></td>
<td align="left"><p>パス、タグ ファイル、またはソースの説明を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377393" data-raw-source="[&lt;strong&gt;SetupGetStringField&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377393)"><strong>SetupGetStringField</strong></a></p></td>
<td align="left"><p>INF ファイル内の指定した行のフィールドからのデータの文字列を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377394" data-raw-source="[&lt;strong&gt;SetupGetTargetPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377394)"><strong>SetupGetTargetPath</strong></a></p></td>
<td align="left"><p>指定した INF ファイルのセクションに記載されているファイルのターゲット パスを決定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377398" data-raw-source="[&lt;strong&gt;SetupInstallFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377398)"><strong>SetupInstallFile</strong></a></p></td>
<td align="left"><p>特定のターゲット ディレクトリに指定されたファイルをインストールします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377399" data-raw-source="[&lt;strong&gt;SetupInstallFileEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377399)"><strong>SetupInstallFileEx</strong></a></p></td>
<td align="left"><p>特定のターゲット ディレクトリに指定されたファイルをインストールします。 既存のバージョンのファイルを使用している場合、インストールは延期されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377400" data-raw-source="[&lt;strong&gt;SetupInstallFilesFromInfSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377400)"><strong>SetupInstallFilesFromInfSection</strong></a></p></td>
<td align="left"><p>キューで指定した INF ファイルはファイルをコピーするためのセクションです。 (同じ<a href="https://msdn.microsoft.com/library/windows/desktop/aa377423" data-raw-source="[&lt;strong&gt;SetupQueueCopySection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377423)"> <strong>SetupQueueCopySection</strong></a>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377401" data-raw-source="[&lt;strong&gt;SetupInstallFromInfSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377401)"><strong>SetupInstallFromInfSection</strong></a></p></td>
<td align="left"><p>INF で指定されたディレクティブを実行します<em>DDInstall</em>セクション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377402" data-raw-source="[&lt;strong&gt;SetupInstallServicesFromInfSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377402)"><strong>SetupInstallServicesFromInfSection</strong></a></p></td>
<td align="left"><p>INF で指定されているサービスのインストールと削除操作を実行します<em>DDInstall</em><strong>します。サービス</strong>セクション。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377407" data-raw-source="[&lt;strong&gt;SetupOpenAppendInfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377407)"><strong>SetupOpenAppendInfFile</strong></a></p></td>
<td align="left"><p>INF ファイルを開き、既存の INF ハンドルに追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377409" data-raw-source="[&lt;strong&gt;SetupOpenInfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377409)"><strong>SetupOpenInfFile</strong></a></p></td>
<td align="left"><p>INF ファイルを開き、ハンドルを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377411" data-raw-source="[&lt;strong&gt;SetupOpenMasterInf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377411)"><strong>SetupOpenMasterInf</strong></a></p></td>
<td align="left"><p>オペレーティング システムの既定のインストールに含まれていたファイルのファイルおよびレイアウト情報を含むマスターの INF ファイルを開きます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377416" data-raw-source="[&lt;strong&gt;SetupQueryInfFileInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377416)"><strong>SetupQueryInfFileInformation</strong></a></p></td>
<td align="left"><p>指定した INF ファイルの構成の INF ファイルのいずれかの名前を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377418" data-raw-source="[&lt;strong&gt;SetupQueryInfVersionInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377418)"><strong>SetupQueryInfVersionInformation</strong></a></p></td>
<td align="left"><p>指定した INF ファイルの構成要素である INF ファイルの 1 つのバージョン番号を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377436" data-raw-source="[&lt;strong&gt;SetupSetDirectoryId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377436)"><strong>SetupSetDirectoryId</strong></a></p></td>
<td align="left"><p>指定されたディレクトリにディレクトリ ID (DIRID) を割り当てます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377446" data-raw-source="[&lt;strong&gt;SetupUninstallOEMInf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377446)"><strong>SetupUninstallOEMInf</strong></a></p></td>
<td align="left"><p>指定した INF ファイルをアンインストールし、関連付けられているを削除します。<em>pnf</em>および<em>。cat</em>ファイル、存在する場合。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377447" data-raw-source="[&lt;strong&gt;SetupVerifyInfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377447)"><strong>SetupVerifyInfFile</strong></a></p></td>
<td align="left"><p>デジタル署名の INF ファイルが変更されていないことを確認します。 (Windows XP 以降)。</p></td>
</tr>
</tbody>
</table>

 

 

 





