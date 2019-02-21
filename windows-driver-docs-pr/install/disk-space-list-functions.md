---
title: ディスク領域の関数の一覧
description: ディスク領域の関数の一覧
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
ms.openlocfilehash: 875f98f96b241c7d90499213c87f89c568cfa9c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539491"
---
# <a name="disk-space-list-functions"></a>ディスク領域の関数の一覧





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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376978" data-raw-source="[&lt;strong&gt;SetupAddInstallSectionToDiskSpaceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376978)"><strong>SetupAddInstallSectionToDiskSpaceList</strong></a></p></td>
<td align="left"><p>検索<strong>CopyFile</strong>と<strong>DelFile</strong>ディレクティブ、 <em>DDInstall</em>セクション、INF ファイルのディスク領域の一覧にこれらのセクションで指定されたファイルの操作を追加。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376979" data-raw-source="[&lt;strong&gt;SetupAddSectionToDiskSpaceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376979)"><strong>SetupAddSectionToDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域一覧が、すべてのファイルをコピーまたは INF ファイルの指定したセクションに記載されている削除の操作を追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376980" data-raw-source="[&lt;strong&gt;SetupAddToDiskSpaceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376980)"><strong>SetupAddToDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域の一覧には、1 つの削除、またはコピー操作を追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376991" data-raw-source="[&lt;strong&gt;SetupCreateDiskSpaceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376991)"><strong>SetupCreateDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域の一覧を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376995" data-raw-source="[&lt;strong&gt;SetupDestroyDiskSpaceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376995)"><strong>SetupDestroyDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域のリストを破棄し、割り当てられているリソースを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377414" data-raw-source="[&lt;strong&gt;SetupQueryDrivesInDiskSpaceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377414)"><strong>SetupQueryDrivesInDiskSpaceList</strong></a></p></td>
<td align="left"><p>ディスク領域の一覧に記載されているファイルの操作で参照されているドライブの一覧では、呼び出し元が指定のバッファーを塗りつぶします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377420" data-raw-source="[&lt;strong&gt;SetupQuerySpaceRequiredOnDrive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377420)"><strong>SetupQuerySpaceRequiredOnDrive</strong></a></p></td>
<td align="left"><p>特定のドライブに記載されているすべてのファイル操作を実行するために必要な空き領域を確認するディスク領域の一覧を検証します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377430" data-raw-source="[&lt;strong&gt;SetupRemoveFromDiskSpaceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377430)"><strong>SetupRemoveFromDiskSpaceList</strong></a></p></td>
<td align="left"><p>コピーまたはディスク領域の一覧から削除する操作をファイルを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377432" data-raw-source="[&lt;strong&gt;SetupRemoveInstallSectionFromDiskSpaceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377432)"><strong>SetupRemoveInstallSectionFromDiskSpaceList</strong></a></p></td>
<td align="left"><p>検索<strong>CopyFiles</strong>と<strong>DelFiles</strong>ディレクティブ、 <em>DDInstall</em>のセクション、INF ファイル、およびディスク領域からこれらのセクションに指定されたファイルの操作を削除します。リスト。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SetupRemoveSectionFromDiskSpaceList</strong></p></td>
<td align="left"><p>ファイルのコピーを一覧表示または削除、INF ファイルの指定されたセクションに記載されている操作をディスク領域から削除します。</p></td>
</tr>
</tbody>
</table>

 

 

 





