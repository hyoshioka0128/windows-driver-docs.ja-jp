---
title: メッセージ コンパイラ タスク
description: Windows Driver Kit (WDK) には、MSBuild を使用してドライバーをビルドするときに、MC.exe ツールを実行できるようにの MessageCompiler タスクが用意されています。 MC.exe を使用する方法の詳細については、メッセージ コンパイラ (MC.exe) を参照してください。
ms.assetid: 77B2DBF4-64EB-4396-BAA5-80F23C9899CC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9ff8bbe41ff03e3392bf439c989ec07b00782cc
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464021"
---
# <a name="message-compiler-task"></a>メッセージ コンパイラ タスク


Windows Driver Kit (WDK) には、MSBuild を使用してドライバーをビルドするときに、MC.exe ツールを実行できるようにの MessageCompiler タスクが用意されています。 MC.exe を使用する方法の詳細については、次を参照してください。 [**メッセージ コンパイラ (MC.exe)**](https://msdn.microsoft.com/library/windows/desktop/aa385638)します。

MSBuild では、MessageCompile 項目を使用して、MessageCompiler タスクのパラメーターを送信します。 MessageCompile 項目では、プロジェクト ファイルで mc.exe の項目メタデータにアクセスします。

次の例では、.vcxproj ファイルのメタデータを編集する方法を示します。

```XML
<ItemGroup>
    <MessageCompile Include="a.mc">
      <GenerateBaselineResource>true</GenerateBaselineResource>
      <BaselineResourcePath>c:\test\</BaselineResourcePath>
    </MessageCompile>
</ItemGroup>
```

次の例は、コマンド ラインの呼び出しを示しています。

```
mc.exe –s "c:\test\" a.mc
```

MSBuild がメタデータ GenerateBaselineResource が設定されているために – s スイッチを使用して、ファイル a.mc mc.exe を呼び出す上記の例で true に設定します。 また、MSBuild は BaselineResourcePath メタデータを使用して、– s スイッチの引数を指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MessageCompiler タスク パラメーター</th>
<th align="left">項目メタデータ</th>
<th align="left">ツールへの切り替え</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ソース</strong>
<p>省略可能な文字列パラメーター。 コンパイルするマニフェスト ファイルの名前を指定します。 コンパイルするメッセージ ファイルの名前を指定します。</p></td>
<td align="left">@(MessageCompile)</td>
<td align="left"><p><strong>&lt;filename.man&gt;</strong></p>
<p><strong>&lt;filename.mc&gt;</strong></p></td>
</tr>
<tr class="even">
<td align="left"><strong>ANSIInputFile</strong>
<p>ANSI (既定値) に、入力ファイルを指定します。</p></td>
<td align="left">%(MessageCompile.ANSIInputFile)</td>
<td align="left"><strong>-</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>ANSIMessageInBinFile</strong>
<p>指定します内のメッセージ、します。BIN ファイルには、ANSI 必要があります。</p></td>
<td align="left">%(MessageCompile.ANSIMessageInBinFile)</td>
<td align="left"><strong>は、</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>EnableDebugOutputPath</strong>
<p>設定されている場合は true。 これにより、– x スイッチ。</p></td>
<td align="left">%(MessageCompile.EnableDebugOutputPath)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>DebugOutputPath</strong>
<p>.Dbg C がコンパイラによって格納されるフォルダーのインクルード ファイルを指定します。 .Dbg ファイルは、メッセージの Id をシンボリック名にマップします。</p></td>
<td align="left">%(MessageCompile.DebugOutputPath)</td>
<td align="left"><strong>-x</strong><em>&lt;パス&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>EnableCallOutMacro</strong>
<p>ログ記録中にユーザー コードを起動する吹き出しマクロを追加します。 このスイッチで有効でないC#は無視されます。</p></td>
<td align="left">%(MessageCompile.EnableCallOutMacro)</td>
<td align="left"><strong>-co</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>EventmanPath</strong>
<p>Eventman.xsd ファイルへのパスを指定します。</p></td>
<td align="left">%(MessageCompile.EventmanPath)</td>
<td align="left"><strong>-w</strong><em>&lt;ファイル&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateBaselineResource</strong>
<p>設定されている場合は true、-s スイッチはすべて有効です。</p></td>
<td align="left">%(MessageCompile.GenerateBaselineResource)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>BaselineResourcePath</strong>
<p>プロバイダーごとのバイナリのリソースを生成します。 概要のグローバル リソース MCGenResource.BIN が生成されます。</p></td>
<td align="left">%(MessageCompile.BaselineResourcePath)</td>
<td align="left"><strong>-s</strong><em>&lt;パス&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateC #LoggingClass</strong>
<p>生成C#(管理) のログ記録クラス FX3.5 イベント クラスに基づいています。</p></td>
<td align="left">%(MessageCompile.GenerateC#LoggingClass)</td>
<td align="left"><strong>-cs</strong><em>&lt;名前空間&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateC #StaticLoggingClass</strong>
<p>静的が生成されますC#(管理) のログ記録クラス FX3.5 イベント クラスに基づいています。</p></td>
<td align="left">%(MessageCompile.GenerateC#StaticLoggingClass)</td>
<td align="left"><strong>-css</strong><em>&lt;namespace&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GeneratedFilesBaseName</strong>
<p>生成されたファイルの基本名を指定します。 既定では入力ファイルのベース名です。</p></td>
<td align="left">%(MessageCompile.GeneratedFilesBaseName)</td>
<td align="left"><strong>-z</strong><em>&lt;basename&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GeneratedHeaderPath</strong>
<p>設定されている場合は true、-h スイッチはすべて有効です。</p></td>
<td align="left">%(MessageCompile.GeneratedHeaderPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>HeaderFilePath</strong>
<p>C のインクルード ファイルを作成する場所のパスを指定します。 既定値は.</p></td>
<td align="left">%(MessageCompile.HeaderFilePath)</td>
<td align="left"><strong>-h</strong><em>&lt;パス&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GeneratedRcAndMessagesPath</strong>
<p>設定されている場合は true、-r スイッチはすべて有効です。</p></td>
<td align="left">%(MessageCompile.GeneratedRcAndMessagesPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>RCFilePath</strong>
<p>RC のパスには、ファイルとそれに含まれるバイナリ メッセージ リソース ファイルが含まれます。 を指定します。 既定値は.</p></td>
<td align="left">%(MessageCompile.RCFilePath)</td>
<td align="left"><strong>-r</strong><em>&lt;パス&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateKernelModeLoggingMacros</strong>
<p>カーネル モードのログ記録のマクロを生成します。</p></td>
<td align="left">%(MessageCompile.GenerateKernelModeLoggingMacros)</td>
<td align="left"><strong>-km</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateMOFFile</strong>
<p>すべての関数と生成されるマクロのダウン レベルのサポートが生成されます。 MOF ファイルは、マニフェストから生成されます。 MOF ファイルがで指定した場所に配置、"-h"スイッチします。</p></td>
<td align="left">%(MessageCompile.GenerateMOFFile)</td>
<td align="left"><strong>-mof</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateOLE2Header</strong>
<p>OLE2 ヘッダー ファイルを生成します。 状態コードの定義ではなく、HRESULT の定義を使用します。</p></td>
<td align="left">%(MessageCompile.GenerateOLE2Header)</td>
<td align="left"><strong>-o</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateUserModeLoggingMacros</strong>
<p>ユーザー モードのログ記録のマクロを生成します。</p></td>
<td align="left">%(MessageCompile.GenerateUserModeLoggingMacros)</td>
<td align="left"><strong>-um</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>HeaderExtension</strong>
<p>ヘッダー ファイル (1 ~ 3 文字) の拡張子を指定します。</p></td>
<td align="left">%(MessageCompile.HeaderExtension)</td>
<td align="left"><strong>-e</strong><em>&lt;拡張機能&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>MaximumMessageLength</strong>
<p>すべてのメッセージのサイズを超えた場合に警告を生成&lt;長さ&gt;文字。</p></td>
<td align="left">%(MessageCompile.MaximumMessageLength)</td>
<td align="left"><strong>-m</strong><em>&lt;長さ&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>PrefixMacroName</strong>
<p>生成されたログ記録マクロに適用される、マクロ名のプレフィックスを定義します。 既定では"EventWrite です"。</p></td>
<td align="left">% (MessageCompile PrefixMacroName)</td>
<td align="left"><strong>-p</strong><em>&lt;プレフィックス&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>RemoveCharsFromSymbolName</strong>
<p>マクロ名が形成する前に削除する各イベントのシンボル名の先頭にテキストを定義します。 既定では NULL です。</p></td>
<td align="left">%(RemoveCharsFromSymbolName)</td>
<td align="left"><strong>-P</strong><em>&lt;プレフィックス&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SetCustomerbit</strong>
<p>メッセージ ID 全体におけるカスタマー ビットを設定します。</p></td>
<td align="left">%(MessageCompile.SetCustomerbit)</td>
<td align="left"><strong>-c</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>TerminateMessageWithNull</strong>
<p>メッセージのテーブルに null 文字を含むすべての文字列を終了します。</p></td>
<td align="left">%(MessageCompile.TerminateMessageWithNull)</td>
<td align="left"><strong>-n</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>UnicodeInputFile</strong>
<p>入力ファイルには Unicode です。</p></td>
<td align="left">%(MessageCompile.UnicodeInputFile)</td>
<td align="left"><strong>-u</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>UnicodeMessageInBinFile</strong>
<p>内のメッセージ。BIN ファイルには、Unicode (既定値) 必要があります。</p></td>
<td align="left">%(MessageCompile.UnicodeMessageInBinFile)</td>
<td align="left"><strong>-U</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>UseBaseNameOfInput</strong>
<p>指定します。箱のファイル名には、.mc ファイル名が一意かどうかに含まれる必要があります。</p></td>
<td align="left">% (MessageCompile します。 UseBaseNameOfInput)</td>
<td align="left"><strong>-b</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>UseDecimalValues</strong>
<p>10 進数のヘッダー ファイルで、FACILTY と重要度の値を指定します。 セットは、10 進数のヘッダーの値を最初にメッセージです。</p></td>
<td align="left">%(MessageCompile.UseDecimalValues)</td>
<td align="left"><strong>-d</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>ValdateAgainstBaselineResource</strong>
<p>これには、-t スイッチを生成し、true に設定されます。 場合、</p></td>
<td align="left">%(MessageCompile.ValdateAgainstBaselineResource)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>BaselinePath</strong>
<p>基準計画のリソースに対して検証します。</p></td>
<td align="left">%(MessageCompile.BaselinePath)</td>
<td align="left"><strong>-t</strong><em>&lt;パス&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>詳細</strong>
<p>詳細な出力を指定します。</p></td>
<td align="left">%(MessageCompile.Verbose)</td>
<td align="left"><strong>-v</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>WinmetaPath</strong>
<p>Winmeta.xml ファイルへのパスを指定します。</p></td>
<td align="left">%(MessageCompile.WinmetaPath)</td>
<td align="left"><strong>-W</strong><em>&lt;ファイル&gt;</em></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**メッセージ コンパイラ (MC.exe)**](https://msdn.microsoft.com/library/windows/desktop/aa385638)

 

 






