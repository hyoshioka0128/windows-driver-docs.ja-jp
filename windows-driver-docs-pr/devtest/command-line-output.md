---
title: コマンドライン出力
description: コマンドライン出力
ms.assetid: 21225785-e8b8-4488-b0a0-fe4cea50d1ff
keywords:
- 出力ファイルは、WDK Static Driver Verifier
- コマンド ライン WDK Static Driver Verifier の出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b0caf66d4f52e3c062f5f4d431e3fbd66d313f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536945"
---
# <a name="command-line-output"></a>コマンドライン出力


SDV のコマンドを送信するときに実行されるコマンドの成否を示すステータス メッセージとエラー メッセージまたは警告が生成されている可能性がありますコマンドに関する情報が表示されます。 出力の下部にある検証の結果の概要が表示されます。

たとえば、次の図と SDV-FailDriver-WDM ドライバーのサンプルを確認するためのコマンドからコマンドライン出力を示しています。、[スピンロック](wdm-spinlock.md)ルール。 SDV の FailDriver-WDM サンプル ドライバーを使用してドライバーを意図的なコーディング エラーにある、\\ツール\\sdv\\サンプル\\Windows ドライバーのサンプルの Sdv の FailDriver-WDM フォルダー。

この検証では、SDV は、ドライバーがルールに違反したことがわかりました。

```
G:\Windows-driver-samples\tools\sdv\samples\SDV-FailDriver-WDM\driver>msbuild /p:Configuration=Release /p:Platform=x64 /t:sdv /p:inputs=/check:spinlock
Microsoft (R) Build Engine version 15.6.82.30579 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 3/30/2018 10:56:50 AM.
Project "G:\Windows-driver-samples\tools\sdv\samples\SDV-FailDriver-WDM\driver\fail_driver1.vcxproj" on node 1 (sdv tar
get(s)).
sdv:
  staticdv /check:spinlock
  SDV: H:\Program Files\Windows Kits\10\TOOLS\SDV
  SMV: H:\Program Files\Windows Kits\10\TOOLS\SDV\smv
  SDVAP: H:\Program Files\Windows Kits\10\TOOLS\SDV\smv\analysisplugins\sdv
  Build environment: msbuild
  [INFO] Cleaning ...
  [INFO] Setting interceptor platform to x64
  [INFO] Setting platform to x86_amd64
  [INFO] Validating XML against schema: H:\Program Files\Windows Kits\10\TOOLS\SDV\smv\bin\Config.xsd
  [INFO] Running local scheduler with 8 threads
  [INFO] Driver type found: wdm
  [INFO] Currently reading and validating XML settings from H:\Program Files\Windows Kits\10\TOOLS\SDV\data\wdm\sdv-def
  ault.xml

  [INFO] 1 of 2 jobs remaining. Avg(s): 8.00. Std.Dev(s): 0.00
  [INFO] 1 of 3 jobs remaining. Avg(s): 9.00. Std.Dev(s): 1.00
  Scan ...Done

  [INFO] 0 of 3 jobs remaining. Avg(s): 6.00. Std.Dev(s): 4.32

  Building ...Done
  [INFO] Using plugin SdvPlugin.SmvSdv for analysis.
  [INFO] Running analysis on 11 precondition(s) & 1 rule(s) ...
  [INFO] Checking preconditions...

  [INFO] 10 of 15 jobs remaining. Avg(s): 7.20. Std.Dev(s): 3.66
  [INFO] 10 of 16 jobs remaining. Avg(s): 7.50. Std.Dev(s): 3.40
  [INFO] 11 of 17 jobs remaining. Avg(s): 7.50. Std.Dev(s): 3.40
  [INFO] 10 of 18 jobs remaining. Avg(s): 9.13. Std.Dev(s): 4.08
  [INFO] 11 of 19 jobs remaining. Avg(s): 9.13. Std.Dev(s): 4.08
  [INFO] 10 of 20 jobs remaining. Avg(s): 11.30. Std.Dev(s): 5.68
  [INFO] 11 of 21 jobs remaining. Avg(s): 11.30. Std.Dev(s): 5.68
  [INFO] 11 of 22 jobs remaining. Avg(s): 12.18. Std.Dev(s): 6.09
  [INFO] 10 of 22 jobs remaining. Avg(s): 11.92. Std.Dev(s): 5.89
  [INFO] 10 of 23 jobs remaining. Avg(s): 12.15. Std.Dev(s): 5.72
  [INFO] 10 of 24 jobs remaining. Avg(s): 12.64. Std.Dev(s): 5.79
  [INFO] 7 of 25 jobs remaining. Avg(s): 13.50. Std.Dev(s): 5.80
  [INFO] 7 of 25 jobs remaining. Avg(s): 13.50. Std.Dev(s): 5.80
  [INFO] 7 of 25 jobs remaining. Avg(s): 13.50. Std.Dev(s): 5.80
  [INFO] 7 of 25 jobs remaining. Avg(s): 13.50. Std.Dev(s): 5.80
  [INFO] 6 of 25 jobs remaining. Avg(s): 13.42. Std.Dev(s): 5.65
  [INFO] 5 of 25 jobs remaining. Avg(s): 13.75. Std.Dev(s): 5.69
  [INFO] 4 of 25 jobs remaining. Avg(s): 13.95. Std.Dev(s): 5.63
  [INFO] 3 of 25 jobs remaining. Avg(s): 14.09. Std.Dev(s): 5.53
  [INFO] 2 of 25 jobs remaining. Avg(s): 14.13. Std.Dev(s): 5.42
  [INFO] 1 of 25 jobs remaining. Avg(s): 14.17. Std.Dev(s): 5.30
  [INFO] 0 of 25 jobs remaining. Avg(s): 14.20. Std.Dev(s): 5.20
  [INFO] Precondition check(s) completed.
  [INFO] Verifying rules...

  [INFO] 1 of 27 jobs remaining. Avg(s): 13.65. Std.Dev(s): 5.78
  [INFO] 1 of 28 jobs remaining. Avg(s): 13.37. Std.Dev(s): 5.86
  [INFO] 0 of 28 jobs remaining. Avg(s): 13.21. Std.Dev(s): 5.81

  [INFO] 1 defects found.
  [INFO] Please review using '/view' argument for SDV.

  [INFO] Total time taken 96 seconds
  [INFO] Found 1 bugs!
Done Building Project "G:\Windows-driver-samples\tools\sdv\samples\SDV-FailDriver-WDM\driver\fail_driver1.vcxproj" (sdv
 target(s)).


Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:01:37.93
```

どのルールに違反しましたを表示する結果の概要を表示した後を指定できます、 **/ビュー**静的ドライバー検証ツールのレポートを表示する MSBuild コマンドのオプション。 コマンド オプションについては、次を参照してください。 [Static Driver Verifier のコマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md)します。 については、**スキャン**、**ビルド**と**確認**出力では、手順を参照してください[検証プロセス](verification-process.md)します。

次の表では、結果の概要に表示される結果について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">結果の型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ルールのパス</strong></p></td>
<td align="left"><p>SDV を検証するをいないことを証明するルールの違反がルールの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>欠陥</strong></p></td>
<td align="left"><p>SDV の検出規則違反の数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>該当なし</strong></p></td>
<td align="left"><p>ドライバーが、分析のために必要なエントリ ポイントをサポートしていないため、または、ドライバーは、ルールを監視する関数を呼び出さなかったため、SDV を確認できませんでしたルールの数。</p>
<p>この値が 0 より大きい場合は、ことを確認します。、 <a href="sdv-map-h.md" data-raw-source="[Sdv-map.h](sdv-map-h.md)">Sdv map.h</a>ファイルの内容が正しい。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>タイムアウト</strong></p></td>
<td align="left"><p>SDV に各規則の検証の制限時間を超えたために検証が停止しているルールの数。 制限時間設定されて、<a href="static-driver-verifier-options-file.md" data-raw-source="[Static Driver Verifier Options File](static-driver-verifier-options-file.md)">静的ドライバー検証ツールのオプション ファイル</a>、Sdv default.xml します。</p>
<p>この結果は、SDV の制限事項が原因です。 ドライバーのエラーは示されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Spaceouts</strong></p></td>
<td align="left"><p>SDV は、検証ルールを検証するためのメモリ制限を超えたために停止ルールの数。 メモリの制限が設定されて、<a href="static-driver-verifier-options-file.md" data-raw-source="[Static Driver Verifier Options File](static-driver-verifier-options-file.md)">静的ドライバー検証ツールのオプション ファイル</a>、Sdv default.xml します。</p>
<p>この結果は、SDV の制限事項が原因です。 ドライバーのエラーは示されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>その他</strong></p></td>
<td align="left"><p>SDV 元となることを復旧できませんでした内部エラーの発生回数。</p></td>
</tr>
</tbody>
</table>

 

 

 





