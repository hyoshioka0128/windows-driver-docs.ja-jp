---
title: ディスク要求およびエラー処理関数
description: ディスク要求およびエラー処理関数
ms.assetid: e1afeeb3-02f0-4570-9910-f948646f07bf
keywords:
- SetupAPI 関数 WDK、ディスクの入力を求める
- SetupAPI 関数 WDK、エラー処理
- エラー WDK SetupAPI
- ディスクの WDK SetupAPI の入力を求める
- ディスクの挿入 WDK SetupAPI の入力を求める
- メディアの WDK SetupAPI の入力を求める
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f88f144aea08b6b9ad71d3fa67c11e46f5d026bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356058"
---
# <a name="disk-prompting-and-error-handling-functions"></a>ディスク要求およびエラー処理関数





一般的なセットアップ関数を使用するには、新しいメディアを挿入したり、ファイルがコピーされるときに発生するエラーを処理するためにユーザー入力を求める名前変更、または削除します。

次の表には、インストール メディアを要求して、エラーの報告 ダイアログ ボックスを提供する関数が一覧表示します。 関数の詳細な説明については、Microsoft Windows SDK のドキュメントを参照してください。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376989" data-raw-source="[&lt;strong&gt;SetupCopyError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376989)"><strong>SetupCopyError</strong></a></p></td>
<td align="left"><p>コピーのエラーのユーザーに通知するダイアログ ボックスを生成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376994" data-raw-source="[&lt;strong&gt;SetupDeleteError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376994)"><strong>SetupDeleteError</strong></a></p></td>
<td align="left"><p>削除エラーのユーザーに通知するダイアログ ボックスを生成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377412" data-raw-source="[&lt;strong&gt;SetupPromptForDisk&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377412)"><strong>SetupPromptForDisk</strong></a></p></td>
<td align="left"><p>インストール中またはソース ファイルの場所をユーザーに求めるダイアログ ボックスを生成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377434" data-raw-source="[&lt;strong&gt;SetupRenameError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377434)"><strong>SetupRenameError</strong></a></p></td>
<td align="left"><p>名前の変更エラーのユーザーに通知するダイアログ ボックスを生成します。</p></td>
</tr>
</tbody>
</table>

 

 

 





