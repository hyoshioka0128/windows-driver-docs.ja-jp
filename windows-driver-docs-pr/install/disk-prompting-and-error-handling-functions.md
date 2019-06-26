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
ms.openlocfilehash: 30a874724506eeb43fc78cd08b1b9cde79f39e5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375323"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcopyerrora" data-raw-source="[&lt;strong&gt;SetupCopyError&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcopyerrora)"><strong>SetupCopyError</strong></a></p></td>
<td align="left"><p>コピーのエラーのユーザーに通知するダイアログ ボックスを生成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdeleteerrora" data-raw-source="[&lt;strong&gt;SetupDeleteError&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdeleteerrora)"><strong>SetupDeleteError</strong></a></p></td>
<td align="left"><p>削除エラーのユーザーに通知するダイアログ ボックスを生成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuppromptfordiska" data-raw-source="[&lt;strong&gt;SetupPromptForDisk&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuppromptfordiska)"><strong>SetupPromptForDisk</strong></a></p></td>
<td align="left"><p>インストール中またはソース ファイルの場所をユーザーに求めるダイアログ ボックスを生成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuprenameerrora" data-raw-source="[&lt;strong&gt;SetupRenameError&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuprenameerrora)"><strong>SetupRenameError</strong></a></p></td>
<td align="left"><p>名前の変更エラーのユーザーに通知するダイアログ ボックスを生成します。</p></td>
</tr>
</tbody>
</table>

 

 

 





