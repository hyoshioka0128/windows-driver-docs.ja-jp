---
title: InfVerif
description: InfVerif (InfVerif) は、ドライバーの INF ファイルをテストするために使用できるツールです。 Inf 構文の問題を報告するだけでなく、INF ファイルがユニバーサルであるかどうかが報告されます。
ms.assetid: 6F565E1C-C6FC-4637-B476-FE4E4672CCC3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce2970f0cd160b627539b0b6bcdf98018b0f32af
ms.sourcegitcommit: 7aa0dc2d0465f815438dcbb5335fd6a77a0fd630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/01/2019
ms.locfileid: "73432666"
---
# <a name="infverif"></a>InfVerif


InfVerif (InfVerif) は、ドライバーの INF ファイルをテストするために使用できるツールです。 Inf 構文の問題を報告するだけでなく、INF ファイルがユニバーサルであるかどうかが報告されます。

> [!NOTE]
> InfVerif は、ChkINF ツールを置き換えます。

Windows Driver Kit (WDK) 10 を使用して Microsoft Visual Studio 2017 でドライバーをビルドすると、コンパイラはビルドプロセスの一部として自動的にツールを実行します。 または、コマンドラインから InfVerif ツールを実行することもできます。

検証ツールは、WDK 10 インストールの一部であり、WDK 10 インストールの \\tools サブディレクトリ、c:\\Program Files (x86)\\Windows キット\\10\\ツール\\にあります。

InfVerif ツールは、次の種類のエラー/警告を報告します。

-   **エラー/警告**(1200-1299): これらの問題によってドライバーパッケージのインストールが妨げられることはありませんが、ドライバーのインストール時に INF の特定の行が実行されていないことを示しています。

-   **INF を非ユニバーサルにする問題。** (1300-1309)

-   **警告**(2000-2999): これらの問題は、常に警告として報告されます。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


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
<td align="left"><p><a href="running-infverif-from-the-command-line.md" data-raw-source="[Running InfVerif from the command line](running-infverif-from-the-command-line.md)">コマンドラインからの InfVerif の実行</a></p></td>
<td align="left"><p>このトピックでは、コマンドラインから InfVerif を実行するときに使用できるオプションの一覧を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="inf-validation-errors-and-warnings.md" data-raw-source="[INF Validation Errors and Warnings](inf-validation-errors-and-warnings.md)">INF 検証エラーと警告</a></p></td>
<td align="left"><p>このトピックでは、Visual Studio が実行する自動 INF 検証の結果として表示されるドライバーのインストールエラーと警告、または InfVerif ツールを実行したときに発生する警告について説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ユニバーサル Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)

[ユニバーサル INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-configurable-inf-file)

 

 






