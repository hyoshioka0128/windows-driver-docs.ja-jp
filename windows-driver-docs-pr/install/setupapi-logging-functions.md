---
title: SetupAPI ログ関数
description: SetupAPI ログ関数
ms.assetid: d27bd44c-41c1-4546-b463-11ed3f5c7d84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a118245ea93182b1c938a4a87f22ae9c00b836c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531351"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552211" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552211)"><strong>SetupGetThreadLogToken</strong></a></p></td>
<td align="left"><p>取得、<a href="log-tokens.md" data-raw-source="[log token](log-tokens.md)">ログ トークン</a>を呼び出したスレッドの<a href="https://msdn.microsoft.com/library/windows/hardware/ff552211" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552211)"> <strong>SetupGetThreadLogToken</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552216" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552216)"><strong>SetupSetThreadLogToken</strong></a></p></td>
<td align="left"><p>呼び出したスレッドのログのトークンを設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff552216" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552216)"> <strong>SetupSetThreadLogToken</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552218" data-raw-source="[&lt;strong&gt;SetupWriteTextLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552218)"><strong>SetupWriteTextLog</strong></a></p></td>
<td align="left"><p>ログ エントリを書き込みます、 <a href="setupapi-text-logs.md" data-raw-source="[SetupAPI text log](setupapi-text-logs.md)">SetupAPI テキスト ログ</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552232" data-raw-source="[&lt;strong&gt;SetupWriteTextLogError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552232)"><strong>SetupWriteTextLogError</strong></a></p></td>
<td align="left"><p>SetupAPI 固有のエラーまたは SetupAPI テキスト ログで Win32 エラーに関する情報を書き込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552236" data-raw-source="[&lt;strong&gt;SetupWriteTextLogInfLine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552236)"><strong>SetupWriteTextLogInfLine</strong></a></p></td>
<td align="left"><p>指定した INF ファイルの行のテキストを含む SetupAPI テキスト ログでログ エントリを書き込みます。</p></td>
</tr>
</tbody>
</table>

 

 

 





