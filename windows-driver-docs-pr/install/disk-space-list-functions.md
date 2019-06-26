---
title: ディスク容量の取得関数
description: ディスク容量の取得関数
ms.assetid: 850e9f41-b534-49f3-891d-c12c1126e52f
keywords:
- SetupAPI 関数 WDK では、ディスク領域を一覧表示します。
- ディスク領域には、WDK SetupAPI が一覧表示されます。
- WDK SetupAPI のディスク領域を計算します。
- WDK SetupAPI 領域の計算
- ディスク領域の計算 WDK SetupAPI
- 合計ディスク領域の計算 WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ada6fe327b1ac6c1e1c78dbdf3abe49e091bd88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375302"
---
# <a name="disk-space-list-functions"></a>ディスク容量の取得関数





ディスク領域の一覧の関数は、作成し、ディスク領域のリストを変更に使用されます。 コピーまたはインストール時に削除されるファイルを処理するために必要な合計ディスク領域を計算するのには、これらのリストを使用できます。

次の表には、ディスク領域のリストを操作するために使用できる関数が一覧表示します。 関数の詳細な説明については、Microsoft Windows SDK のドキュメントを参照してください。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddinstallsectiontodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddInstallSectionToDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddinstallsectiontodiskspacelista)"><strong>SetupAddInstallSectionToDiskSpaceList</strong></a></p></td>
<td align="left"><p>検索<strong>CopyFile</strong>と<strong>DelFile</strong>ディレクティブ、 <em>DDInstall</em>セクション、INF ファイルのディスク領域の一覧にこれらのセクションで指定されたファイルの操作を追加。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddsectiontodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddSectionToDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddsectiontodiskspacelista)"><strong>SetupAddSectionToDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域一覧が、すべてのファイルをコピーまたは INF ファイルの指定したセクションに記載されている削除の操作を追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddtodiskspacelista" data-raw-source="[&lt;strong&gt;SetupAddToDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddtodiskspacelista)"><strong>SetupAddToDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域の一覧には、1 つの削除、またはコピー操作を追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcreatediskspacelista" data-raw-source="[&lt;strong&gt;SetupCreateDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcreatediskspacelista)"><strong>SetupCreateDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域の一覧を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdestroydiskspacelist" data-raw-source="[&lt;strong&gt;SetupDestroyDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdestroydiskspacelist)"><strong>SetupDestroyDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域のリストを破棄し、割り当てられているリソースを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupquerydrivesindiskspacelista" data-raw-source="[&lt;strong&gt;SetupQueryDrivesInDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupquerydrivesindiskspacelista)"><strong>SetupQueryDrivesInDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域の一覧に記載されているファイルの操作で参照されているドライブの一覧では、呼び出し元が指定のバッファーを塗りつぶします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryspacerequiredondrivea" data-raw-source="[&lt;strong&gt;SetupQuerySpaceRequiredOnDrive&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryspacerequiredondrivea)"><strong>SetupQuerySpaceRequiredOnDrive</strong></a></p></td>
<td align="left"><p>特定のドライブに記載されているすべてのファイル操作を実行するために必要な空き領域を確認するディスク領域の一覧を検証します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremovefromdiskspacelista" data-raw-source="[&lt;strong&gt;SetupRemoveFromDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremovefromdiskspacelista)"><strong>SetupRemoveFromDiskSpaceList</strong></a></p></td>
<td align="left"><p>コピーまたはディスク領域の一覧から削除する操作をファイルを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremoveinstallsectionfromdiskspacelista" data-raw-source="[&lt;strong&gt;SetupRemoveInstallSectionFromDiskSpaceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremoveinstallsectionfromdiskspacelista)"><strong>SetupRemoveInstallSectionFromDiskSpaceList</strong></a></p></td>
<td align="left"><p>検索<strong>CopyFiles</strong>と<strong>DelFiles</strong>ディレクティブ、 <em>DDInstall</em>のセクション、INF ファイル、およびディスク領域からこれらのセクションに指定されたファイルの操作を削除します。リスト。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SetupRemoveSectionFromDiskSpaceList</strong></p></td>
<td align="left"><p>ファイルのコピーを一覧表示または削除、INF ファイルの指定されたセクションに記載されている操作をディスク領域から削除します。</p></td>
</tr>
</tbody>
</table>

 

 

 





