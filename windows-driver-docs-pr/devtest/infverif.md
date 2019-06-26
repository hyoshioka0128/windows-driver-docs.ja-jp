---
title: InfVerif
description: InfVerif (InfVerif.exe) は、ドライバーの INF ファイルをテストするのに使用できるツールです。 INF 構文の問題の報告、だけでなく、ツールは、INF ファイルがユニバーサルを報告します。
ms.assetid: 6F565E1C-C6FC-4637-B476-FE4E4672CCC3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e90e3fc5057b0c038bdb69ea9b0d9a28342f237
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354799"
---
# <a name="infverif"></a>InfVerif


InfVerif (InfVerif.exe) は、ドライバーの INF ファイルをテストするのに使用できるツールです。 INF 構文の問題の報告、だけでなく、ツールは、INF ファイルがユニバーサルを報告します。

> [!NOTE]
> InfVerif は、ChkINF ツールを置き換えます。

Windows Driver Kit (WDK) 10 と Microsoft Visual Studio 2017 でドライバーをビルドすると、コンパイラ ツールを実行、自動的にビルド プロセスの一部として。 または、コマンドラインから InfVerif.exe ツールを実行できます。

検証ツールは、WDK 10 のインストールの一部でありで見つかる、 \\、WDK 10 のインストールの tools サブディレクトリ c:\\%program files (x86)\\Windows キット\\10\\ツール\\.

InfVerif ツールでは、次の種類のエラー/警告を報告します。

-   **エラー/警告**(1200 1299)。これらの問題が妨げられない、ドライバー パッケージがインストールされているが、ドライバーがインストールされているときに、INF の特定の行の実行はされていないことを示している操作を行います。

-   **非ユニバーサル、INF を構成する問題です。** (1300-1309)

-   **警告**(2000 ~ 2999)。これらの問題は、常に警告として報告します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="running-infverif-from-the-command-line.md" data-raw-source="[Running InfVerif from the command line](running-infverif-from-the-command-line.md)">コマンドラインから実行中の InfVerif</a></p></td>
<td align="left"><p>このトピックでは、コマンドラインから InfVerif.exe を実行するときに使用できるオプションを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="inf-validation-errors-and-warnings.md" data-raw-source="[INF Validation Errors and Warnings](inf-validation-errors-and-warnings.md)">INF 検証エラーと警告</a></p></td>
<td align="left"><p>このトピックでは、ドライバーのインストール エラーを説明しますと、Visual Studio で自動 INF 検証の結果として表示される警告の実行または InfVerif ツールを実行するとします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ユニバーサル Windows ドライバーをインストールします。](https://docs.microsoft.com/windows-hardware/drivers)

[ユニバーサル INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-configurable-inf-file)

 

 






