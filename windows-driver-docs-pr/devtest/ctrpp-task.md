---
title: Ctrpp タスク
description: Windows Driver Kit (WDK) には、MSBuild を使用してドライバーをビルドするときに、ctrpp.exe ツールを実行できるようにの Ctrpp タスクが用意されています。
ms.assetid: DB457500-5BFF-4488-95EB-EEB3F63947C1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8989e988f12be06b037ecc580c5352b78d201970
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356622"
---
# <a name="ctrpp-task"></a>Ctrpp タスク


Windows Driver Kit (WDK) には、MSBuild を使用してドライバーをビルドするときに、ctrpp.exe ツールを実行できるようにの Ctrpp タスクが用意されています。 Ctrpp.exe の使用方法の詳細については、次を参照してください。 [ **CTRPP**](https://msdn.microsoft.com/library/windows/desktop/aa372128)します。

MSBuild では、Ctrpp 項目を使用して、ctrpp.exe に Ctrpp タスクのパラメーターを送信します。 プロジェクト ファイルで Ctrpp 項目では、ctrpp.exe の項目メタデータにアクセスします。

次の例では、.vcxproj ファイルのメタデータを編集する方法を示します。

```XML
<ItemGroup>
    <Ctrpp Include="a.manifest">
      <GenerateHeaderFileForCounter>true</GenerateHeaderFileForCounter>
      <HeaderFileNameForCounter>c:\test\abc.h</HeaderFileNameForCounter>
    </Ctrpp>
</ItemGroup>
```

次の例は、コマンド ラインの呼び出しを示しています。

```
ctrpp.exe –ch "c:\test\abc.h" a.manifest
```

MSBuild がで ctrpp.exe ファイル a.manifest でを呼び出す上記の例では、 **– ch**メタデータ GenerateHeaderFileForCounter が設定されているためにのオプションを true にします。 MSBuild は HeaderFileNameForCounter メタデータを使用して、引数を指定することも、 **– ch**オプション

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Ctrpp タスク パラメーター</th>
<th align="left">項目メタデータ</th>
<th align="left">ツールへの切り替え</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ソース</td>
<td align="left">@(Ctrpp)</td>
<td align="left"></td>
<td align="left">ITaskItem の必須パラメーターです。 処理するカウンター マニフェストを指定します。</td>
</tr>
<tr class="even">
<td align="left">AddPrefix</td>
<td align="left">%(Ctrpp.AddPrefix)</td>
<td align="left"><strong>-プレフィックス</strong><em>&lt;プレフィックス&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 関数および生成された変数に追加するプレフィックスを指定します。</td>
</tr>
<tr class="odd">
<td align="left">下位互換性</td>
<td align="left">%(Ctrpp.BackwardCompatibility)</td>
<td align="left"><strong>-backcompat</strong></td>
<td align="left">省略可能なブール型パラメーター。 Windows 7 よりも前のオペレーティング システムとバイナリの互換性のあるコードを生成します。</td>
</tr>
<tr class="even">
<td align="left">EnableLegacy</td>
<td align="left">%(Ctrpp.EnableLegacy)</td>
<td align="left"><strong>レガシ</strong></td>
<td align="left">省略可能なブール型パラメーター。 以前の ctrpp ファイルに戻ります。 このスイッチが 4 つの出力ファイルを生成する ctrpp: 2 つのヘッダー ファイル、リソース ファイル、およびソース コード ファイル。 これは、ctrpp の以前のバージョンで見られる動作を模倣します。 -レガシと組み合わせて、-o、ch--rc とプレフィックスのオプションを使用できません。</td>
</tr>
<tr class="odd">
<td align="left">GeneratedCounterFilesPath</td>
<td align="left">%(Ctrpp.GeneratedCounterFilesPath)</td>
<td align="left"><strong>-sumPath</strong><em>&lt;path&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 カウンターのバイナリ ファイルの既定値を生成するパスを指定します。</td>
</tr>
<tr class="even">
<td align="left">GenerateHeaderFileForCounter</td>
<td align="left">%(Ctrpp.GenerateHeaderFileForCounter)</td>
<td align="left"></td>
<td align="left">設定されている場合は true、-ch スイッチはすべて有効です。</td>
</tr>
<tr class="odd">
<td align="left">HeaderFileNameForCounter</td>
<td align="left">%(Ctrpp.HeaderFileNameForCounter)</td>
<td align="left"><strong>-ch</strong><em>&lt;filename&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 カウンターの名前と id を含むヘッダー ファイルを生成します。</td>
</tr>
<tr class="even">
<td align="left">GenerateHeaderFileForProvider</td>
<td align="left">%(Ctrpp.GenerateHeaderFileForProvider)</td>
<td align="left"></td>
<td align="left">設定されている場合は true、-o スイッチはすべて有効です。</td>
</tr>
<tr class="odd">
<td align="left">HeaderFileNameForProvider</td>
<td align="left">%(Ctrpp.HeaderFileNameForProvider)</td>
<td align="left"><strong>-o</strong><em>&lt;ファイル名&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 プロバイダーのヘッダー ファイルを生成します。</td>
</tr>
<tr class="even">
<td align="left">GenerateMemoryRoutines</td>
<td align="left">%(Ctrpp.GenerateMemoryRoutines)</td>
<td align="left"><strong>-MemoryRoutines</strong></td>
<td align="left">省略可能なブール型パラメーター。 メモリの割り当てと解放の日常的なテンプレートを生成します。</td>
</tr>
<tr class="odd">
<td align="left">GenerateNotificationCallback</td>
<td align="left">%(Ctrpp.GenerateNotificationCallback)</td>
<td align="left"><strong>-NotificationCallback</strong></td>
<td align="left">省略可能なブール型パラメーター。 カスタマイズした通知コールバックのテンプレートを生成します。 "Callback"属性と似ています、&lt;プロバイダー&gt;要素。</td>
</tr>
<tr class="even">
<td align="left">GenerateResourceSourceFile</td>
<td align="left">%(Ctrpp.GenerateResourceSourceFile)</td>
<td align="left"></td>
<td align="left">設定されている場合は true、-rc はすべて有効スイッチします。</td>
</tr>
<tr class="odd">
<td align="left">ResourceFileName</td>
<td align="left">%(Ctrpp.ResourceFileName)</td>
<td align="left"><strong>-rc</strong><em>&lt;filename&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 リソースのソース ファイルを生成します。</td>
</tr>
<tr class="even">
<td align="left">GenerateSummaryGlobalFile</td>
<td align="left">%(Ctrpp.GeneratedSummaryGlobalFile)</td>
<td align="left"><strong>-概要</strong><em>&lt;パス&gt;</em></td>
<td align="left">省略可能な文字列パラメーター。 プロバイダーごとにカウンター バイナリ ファイルが生成されます GenSumResource.BIN 概要グローバル ファイルを生成します。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**CTRPP**](https://msdn.microsoft.com/library/windows/desktop/aa372128)
