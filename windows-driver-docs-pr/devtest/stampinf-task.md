---
title: Stampinf タスク
description: Windows Driver Kit (WDK) には、MSBuild を使用してドライバーをビルドするときに、stampinf.exe ツールを実行できるようにの StampInf タスクが用意されています。 Stampinf.exe ツールについては、Stampinf を参照してください。
ms.assetid: 4BD937D3-97C7-408D-9372-F01CBB7B0B62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c3bd71fcf98d267647c0c42f8012f94bdc949d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551415"
---
# <a name="stampinf-task"></a>Stampinf タスク


Windows Driver Kit (WDK) には、MSBuild を使用してドライバーをビルドするときに、stampinf.exe ツールを実行できるようにの StampInf タスクが用意されています。 Stampinf.exe ツールについては、次を参照してください。 [Stampinf](stampinf.md)します。

Inf 項目は、StampInf タスクのパラメーターを送信します。 Stampinf の項目メタデータは、プロジェクト ファイルの Inf を使用してアクセスされます。

次の例はどのように .vcxproj ファイルのメタデータの編集。

```XML
<ItemGroup>
    <Inf Include="a.inf">
      <SpecifyArchitecture>true</SpecifyArchitecture>
      <Architecture>x86</Architecture>
    </Inf>
    <Inf Include="b.inf">
      <SpecifyArchitecture>false</SpecifyArchitecture>
      <Architecture>amd64</Architecture>
    </Inf>
</ItemGroup>
```

次の例は、コマンド ラインの呼び出しを示しています。

```
stampinf.exe –a "x86" a.inf
stampinf.exe b.inf
```

上記の例では、MSBuild は stampinf.exe a.inf と b.inf の両方で、さまざまなパラメーター セットを呼び出します。 B.inf、場合でも、**アーキテクチャ**メタデータが指定されて、 **SpecifyArchitecture**メタデータが false に設定します。 そのため、 **– a**でコマンド ライン スイッチが有効になっていません。 このメタデータを設定した場合**TRUE**が有効になりますし、 **– a amd64**コマンドラインでします。 この方法では、このメタデータを切り替えるだけと、アーキテクチャ メタデータ自体を編集する必要はありません。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">StampInf タスク パラメーター</th>
<th align="left">項目メタデータ</th>
<th align="left">ツールへの切り替え</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ソース</strong>
<p>ITaskItem の必須パラメーターです。 ソース ファイルの一覧を指定します。</p></td>
<td align="left">%(Inf.OutputPath)%(Inf.FileName).inf</td>
<td align="left"><strong>-f</strong><em>[ソース]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>SpecifyArchitecture</strong>
<p>場合のスイッチを有効にこれが true に設定します。</p></td>
<td align="left">%(Inf.SpecifyArchitecture)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>アーキテクチャ</strong>
<p>省略可能な文字列パラメーター。 ターゲット プラットフォームのアーキテクチャを指定します。</p></td>
<td align="left">%(Inf.Architecture)</td>
<td align="left"><strong>-</strong><em>[アーキテクチャ]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>CatalogFile</strong>
<p>省略可能な文字列パラメーター。 INF セクションでは、カタログ ファイルのディレクティブを指定します。</p></td>
<td align="left">%(Inf.CatalogFileName)</td>
<td align="left"><strong>-c</strong><em>&lt;catalogFile&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SpecifyDriverVerDirectiveDate</strong>
<p>これにより、– d スイッチ場合は true に設定します。</p></td>
<td align="left">%(Inf.SpecifyDriverVerDirectiveDate)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>DriverVerDirectiveDate</strong>
<p>省略可能な文字列</p></td>
<td align="left">%(Inf.DateStamp)</td>
<td align="left"><strong>-d</strong><em>[date|<em>]</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>DriverVerDirectiveSection</strong>
<p>省略可能な文字列パラメーター。 INF DriverVer ディレクティブを配置する INF セクションを指定します。</p></td>
<td align="left">%(Inf.DriverVersionSectionName)</td>
<td align="left"><strong>-s</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>SpecifyDriverVerDirectiveVersion</strong>
<p>場合、– v スイッチを有効にこれが true に設定します。</p></td>
<td align="left">%(Inf.SpecifyDriverDirectiveVersion)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>DriverVerDirectiveVersion</strong>
<p>省略可能な文字列パラメーター。 ドライバーのディレクティブでは、バージョン番号を指定します。</p></td>
<td align="left">%(Inf.TimeStamp)</td>
<td align="left"><strong>-v</strong><em>[time|</em>]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>KmdfVersion</strong>
<p>省略可能な文字列パラメーター。 このドライバーが依存する KMDF のバージョンを指定します。</p></td>
<td align="left">%(Inf.KmdfVersionNumber)</td>
<td align="left"><strong>-k</strong><em>&lt;バージョン&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>省略可能なブール型パラメーター。 True の場合、追跡対象のインクリメンタル ビルドが実行されます。 それ以外の場合、再構築が実行されます。</p></td>
<td align="left">%(Inf.MinimalRebuildFromTracking)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolPath</strong>
<p>省略可能な文字列パラメーター。 ツールがあるフォルダーへの完全パスを指定することができます。</p></td>
<td align="left">$(StampInfToolPath)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>省略可能な文字列パラメーター。 書き込む tlog の追跡ツールのログ ディレクトリを指定します。</p></td>
<td align="left">%(Inf.StampInfTrackerLogDirectory)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackFileAccess</strong>
<p>省略可能なブール型パラメーター。 True の場合は、このタスクのファイル アクセスのパターンを追跡します。</p></td>
<td align="left">$(TrackFileAccess)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>UmdfVersion</strong>
<p>省略可能な文字列パラメーター。 UMDF ドライバーが依存しているのバージョンを指定します。</p></td>
<td align="left">%(Inf.UmdfVersionNumber)</td>
<td align="left"><strong>-u</strong><em>&lt;バージョン&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>詳細度</strong>
<p>省略可能なブール型パラメーター。 Stampinf 出力の詳細度を有効にします。</p></td>
<td align="left">%(Inf.EnableVerbose)</td>
<td align="left"><strong>-n</strong></td>
</tr>
</tbody>
</table>

 

 

 





