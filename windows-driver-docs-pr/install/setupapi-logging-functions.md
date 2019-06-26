---
title: SetupAPI ログ関数
description: SetupAPI ログ関数
ms.assetid: d27bd44c-41c1-4546-b463-11ed3f5c7d84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e228720c9372bcb6352a3f03f617b8a1776b40
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386391"
---
# <a name="setupapi-logging-functions"></a>SetupAPI ログ関数


ログ エントリを記述する次の関数を使用できます以降では、Windows Vista、プラグ アンド プレイ (PnP) デバイスのインストール アプリケーション、クラスのインストーラー、および共同インストーラー、 [SetupAPI テキスト ログ](setupapi-text-logs.md)します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)"><strong>SetupGetThreadLogToken</strong></a></p></td>
<td align="left"><p>取得、<a href="log-tokens.md" data-raw-source="[log token](log-tokens.md)">ログ トークン</a>を呼び出したスレッドの<a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)"> <strong>SetupGetThreadLogToken</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)"><strong>SetupSetThreadLogToken</strong></a></p></td>
<td align="left"><p>呼び出したスレッドのログのトークンを設定<a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)"> <strong>SetupSetThreadLogToken</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog" data-raw-source="[&lt;strong&gt;SetupWriteTextLog&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)"><strong>SetupWriteTextLog</strong></a></p></td>
<td align="left"><p>ログ エントリを書き込みます、 <a href="setupapi-text-logs.md" data-raw-source="[SetupAPI text log](setupapi-text-logs.md)">SetupAPI テキスト ログ</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror" data-raw-source="[&lt;strong&gt;SetupWriteTextLogError&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)"><strong>SetupWriteTextLogError</strong></a></p></td>
<td align="left"><p>SetupAPI 固有のエラーまたは SetupAPI テキスト ログで Win32 エラーに関する情報を書き込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline" data-raw-source="[&lt;strong&gt;SetupWriteTextLogInfLine&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)"><strong>SetupWriteTextLogInfLine</strong></a></p></td>
<td align="left"><p>指定した INF ファイルの行のテキストを含む SetupAPI テキスト ログでログ エントリを書き込みます。</p></td>
</tr>
</tbody>
</table>

 

 

 





