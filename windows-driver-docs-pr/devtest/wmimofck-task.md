---
title: Wmimofck タスク
description: Windows Driver Kit (WDK) には、MSBuild を使用して、ドライバーをビルドするときに、wmimofck.exe ツールを実行できるようにの Wmimofck タスクが用意されています。
ms.assetid: 33C5C079-510F-4BD3-AEF1-F152E88E45C2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29295c3d39d4c87b1b0bc5a4cd0345d1bc8bca2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379125"
---
# <a name="wmimofck-task"></a>Wmimofck タスク


Windows Driver Kit (WDK) には、MSBuild を使用して、ドライバーをビルドするときに、wmimofck.exe ツールを実行できるようにの Wmimofck タスクが用意されています。

Wmimofck ツールの使用方法の詳細については、次を参照してください。[を使用して Wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)します。

MSBuild では、Wmimofck 項目を使用して、Wmimofck タスクのパラメーターを送信します。 Wmimofck の項目メタデータは、プロジェクト ファイルで Wmimofck 項目を使用してアクセスします。

次の例では、.vcxproj ファイル内のメタデータを編集する方法を示します。

```XML
<ItemGroup>
    <Wmimofck Include="a.bmf">
      <GenerateStructureDefinitionsForDatablocks>true</GenerateStructureDefinitionsForDatablocks>
    </Wmimofck>
    <Wmimofck Include="b.bmf">
      <HeaderOutputFile>b.h</HeaderOutputFile>
    </Wmimofck>
</ItemGroup>
```

次の例では、コマンド プロンプト ウィンドウで Wmimofck.exe を実行する方法を示しています。

```
Wmimofck.exe -u a.bmf
Wmimofck.exe –h"b.h" b.bmf
```

上記の例では、wmimofck.exe a.bmf と b.bmf の両方で、さまざまなパラメーター セットとさまざまなメタデータを呼び出します。 そのため、スイッチはこれらの入力のさまざまなできます。 つまり、各入力メタデータの独自のセットを呼び出すことができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Wmimofck タスク パラメーター</th>
<th align="left">項目メタデータ</th>
<th align="left">ツールへの切り替え</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ソース</strong>
<p>ITaskItem の必須パラメーターです。 入力ソース ファイルを指定します。</p></td>
<td align="left">@(Wmimofck)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateStructureDefinitionsForDatablocks</strong>
<p>省略可能なブール型パラメーター。 Wmimofck は、MaxLen 修飾子を指定する省略可能なプロパティを含む、固定サイズのあるすべてのプロパティのメンバーの定義を生成します。</p></td>
<td align="left">%(Wmimofck.GenerateStructureDefinitionsForDatablocks)</td>
<td align="left"><strong>-u</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateStructureDefinitionsForMethodParameters</strong>
<p>省略可能なブール型パラメーター。 ヘッダー ファイルには、入力と各 WMI メソッドの出力の構造体の定義が含まれています。</p></td>
<td align="left">%(Wmimofck.GenerateStructureDefinitionsForMethodParameters)</td>
<td align="left"><strong>-m</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>HeaderOutputFile</strong>
<p>省略可能な文字列パラメーター。 ヘッダー ファイルの MOF の定義との同期を維持するために使用する C 言語のヘッダー ファイル (.h ファイル) を生成します。</p></td>
<td align="left">%(Wmimofck.HeaderOutputFile)</td>
<td align="left"><strong>-h</strong><em>ファイル名</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>HexdumpOutputFile</strong>
<p>省略可能な文字列パラメーター。 実行時に動的な MOF データを提供するためのドライバー ソースに含まれる .bmf データの 16 進数のバージョンを生成します。</p></td>
<td align="left">%(Wmimofck.HexdumpOutputFile)</td>
<td align="left"><strong>-x</strong><em>Filename</em></td>
</tr>
<tr class="even">
<td align="left"><strong>HTMLUIOutputDirectory</strong>
<p>設定されている場合は true、-w スイッチはすべて生成します。</p></td>
<td align="left">%(Wmimofck.HTMLUIOutputDirectory)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>HTMLOutputDirectory</strong>
<p>省略可能な文字列パラメーター。 Wmimofck によって生成される HTML ファイルのディレクトリを指定します。</p></td>
<td align="left">%(Wmimofck.HTMLOutputDirectory)</td>
<td align="left"><strong>-w</strong><em>ディレクトリ</em></td>
</tr>
<tr class="even">
<td align="left"><strong>MFLFile</strong>
<p>省略可能な文字列パラメーター。 修正済みのクラスを含むファイルを指定します。</p></td>
<td align="left">%(Wmimofck.MFLFile)</td>
<td align="left"><strong>-z</strong><em>MFLFile</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>省略可能なブール型パラメーター。 True の場合、追跡対象のインクリメンタル ビルドが実行されます。false の場合、再構築を実行します。</p></td>
<td align="left">%(Wmimofck.MinimalRebuildFromTracking)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>MOFFile</strong>
<p>省略可能な文字列パラメーター。 言語に依存しない WMI クラスの宣言を含むファイルを指定します。</p></td>
<td align="left">%(Wmimofck.MOFFile)</td>
<td align="left"><strong>-y</strong><em>MOFFile</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SourceOutputFile</strong>
<p>省略可能な文字列パラメーター。 WMI ドライバー コードのスタブが含まれている C 言語のソース ファイルを生成します。</p></td>
<td align="left">%(Wmimofck.SourceOutputFile)</td>
<td align="left"><strong>-c</strong><em>ファイル名</em></td>
</tr>
<tr class="even">
<td align="left"><strong>TLogReadFiles</strong>
<p>省略可能な文字列パラメーター。</p></td>
<td align="left">@(WmimofckTLogReadFiles)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TLogWriteFiles</strong>
<p>省略可能な文字列パラメーター。</p></td>
<td align="left">@(WmimofckTLogWriteFiles)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolExe</strong>
<p>省略可能な文字列パラメーター。</p></td>
<td align="left">$(WmimofckToolExe)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>ToolPath</strong>
<p>省略可能な文字列パラメーター。 ツールがあるフォルダーへの完全パスを指定します。</p></td>
<td align="left">$(WmimofckToolPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>省略可能な文字列パラメーター。 書き込む tlog の追跡ツールのログ ディレクトリを指定します。</p></td>
<td align="left">%(Wmimofck.TrackerLogDirectory)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackFileAccess</strong>
<p>省略可能なブール型パラメーター。 True の場合は、このタスクのファイル アクセスのパターンを追跡します。</p></td>
<td align="left">$(TrackFileAccess)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolArchitecture</strong>
<p>省略可能な文字列パラメーター。</p></td>
<td align="left">$(WmimofckToolArchitecture)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerFrameworkPath</strong>
<p>省略可能な文字列パラメーター。</p></td>
<td align="left">$(WmimofckTrackerFrameworkPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackerSdkPath</strong>
<p>省略可能な文字列パラメーター。</p></td>
<td align="left">$(WmimofckTrackerSdkPath)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>VBScriptTestOutputFile</strong>
<p>省略可能な文字列パラメーター。 すべてのデータ ブロックと MOF ファイルで指定したプロパティを照会する VBScript プログラムを作成します。</p></td>
<td align="left">%(Wmimofck.VBScriptTestOutputFile)</td>
<td align="left"><strong>-t</strong><em>ファイル名</em></td>
</tr>
<tr class="even">
<td align="left"><strong>AdditionalOptions</strong>
<p>省略可能な文字列パラメーター。</p></td>
<td align="left">%(Wmimofck.AdditionalOptions)</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Wmimofck.exe を使用します。](https://msdn.microsoft.com/library/windows/hardware/ff565588)

 

 






