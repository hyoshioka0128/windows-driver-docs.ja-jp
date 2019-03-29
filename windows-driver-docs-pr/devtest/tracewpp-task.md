---
title: TraceWPP タスク
description: Windows Driver Kit (WDK) には、MSBuild を使用してドライバーをビルドするときに、tracewpp.exe ツールを実行できるようにの TraceWPP タスクが用意されています。
ms.assetid: 74CE1912-8D1D-417E-8B29-36B2AB0253EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 908b3fe9a66ae0b216d6c1c4f8312d0e19f4189a
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350285"
---
# <a name="tracewpp-task"></a>TraceWPP タスク


Windows Driver Kit (WDK) には、MSBuild を使用してドライバーをビルドするときに、tracewpp.exe ツールを実行できるようにの TraceWPP タスクが用意されています。 Tracewpp.exe ツールが実装するために使用される[WPP ソフトウェア トレース](wpp-software-tracing.md)します。

WppEnabled は、ソース ファイルのトレースを有効にする ClCompile 項目に新しいメタデータです。 Wpp タスクは、全体の ClCompile 項目コレクションを実行しに WppEnabled メタデータを設定する対象の各項目に対して tracewpp.exe を呼び出します**TRUE**します。

WppEnabled メタデータは、この case .c、.cpp、.h ファイルで、CL タスクと同じ型の入力ファイルで、WPP タスクが実行されるので、ClCompile 項目に追加されました。

**注**ClCompile 項目をプロジェクト ファイルを使用して tracewpp の項目メタデータにアクセスします。 MSBuild では、ターゲット内で内部的に TraceWpp 項目を使用して、タスクに渡すことです。

 

次の例では、.vcxproj ファイルのメタデータを編集する方法を示します。

```XML
<ItemGroup>
    <ClCompile Include="a.c" />
      <WppEnabled>false</WppEnabled>
    <ClCompile Include="b.c">
        <WppEnabled>true</WppEnabled>
        <WppKernelMode>true</WppKernelMode>
        <WppAdditionalIncludeDirectories>c:\test\</WppAdditionalIncludeDirectories>
    </ClCompile>
    <ClCompile Include="test1.c" />
    <ClCompile Include="test2.c">
        <WppEnabled>true</WppEnabled>
        <WppDllMacro>true</WppDllMacro>
    </ClCompile>
</ItemGroup>
```

コマンド ラインの呼び出しは次のようになります。

```
tracewpp.exe  km /Ic:\test\b.c
tracewpp.exe  dll test2.c
```

上記の例は、MSBuild を呼び出すことを示しています。 **tracewpp.exe** b.c および test2.c でのみため、 **WppEnabled**にメタデータが設定されている**TRUE**のこれらの入力。 また、これら 2 つの入力のメタデータが異なることに注意してください。 そのため、スイッチはこれらの入力のさまざまなできます。 つまり、各入力メタデータの独自のセットを呼び出すことができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP タスク パラメーター</th>
<th align="left">項目メタデータ</th>
<th align="left">ツールへの切り替え</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ソース</strong>
<p>ITaskItem の必須パラメーターです。 ソース ファイルの一覧を指定します。</p></td>
<td align="left">@(TraceWpp)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>AddAlternateNameToMessageGUID</strong>
<p>省略可能な文字列パラメーター。 このトレース プロバイダーから送信されるメッセージのメッセージの GUID の別の表示名を指定します。</p></td>
<td align="left">%(TraceWpp.WppAddAlternateNameToMessageGUID)</td>
<td align="left"><strong>-/o:</strong><em>文字列</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>AdditionalConfigurationFile</strong>
<p>省略可能な文字列パラメーター。 追加の構成ファイルを指定します。 WPP は、指定したファイルを使用して、既定のファイルだけでなく defaultwpp.ini します。</p></td>
<td align="left">%(TraceWpp.WppAdditionalConfigurationFile)</td>
<td align="left"><strong>-ini:</strong><em>パス</em></td>
</tr>
<tr class="even">
<td align="left"><strong>AdditionalIncludeDirectories</strong>
<p>省略可能な string[] 型のパラメーター。 WPP インクルード ファイルを検索するディレクトリの一覧には、ディレクトリを追加します。</p></td>
<td align="left">%(TraceWpp.WppAdditionalIncludeDirectories)</td>
<td align="left"><strong>-</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>AlternateConfigurationFile</strong>
<p>省略可能な文字列パラメーター。 代替の構成ファイルを指定します。 WPP は、defaultwpp.ini ファイルではなくこのファイルを使用します。</p></td>
<td align="left">%(TraceWpp.WppAlternateConfigurationFile)</td>
<td align="left"><strong>-defwpp:</strong><em>パス</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateUsingTemplateFile</strong>
<p>省略可能な文字列パラメーター。 中かっこの間に指定された名前の WPP を処理するすべてのソース ファイルの{}WPP は、指定したファイル名拡張子を持つ別のファイルを作成します。</p></td>
<td align="left">%(TraceWpp.WppGenerateUsingTemplateFile)</td>
<td align="left"><strong>-gen{</strong><em>File.tpl</em><strong>}*.ext</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>省略可能なブール型パラメーター。 値が場合<strong>TRUE</strong>WPP は追跡対象のインクリメンタル ビルドを実行します。 それ以外の場合、WPP は再構築を実行します。</p></td>
<td align="left">%(TraceWpp.WppMinimalRebuildFromTracking)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>NumericBaseForFormatStrings</strong>
<p>Int 型の省略可能なパラメーターです。 書式指定文字列の番号付けの数値の基数を確立します。</p></td>
<td align="left">%(TraceWpp.WppNumericBaseForFormatStrings)</td>
<td align="left"><strong>-argbase:</strong><em>数</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>AddControlGUID</strong>
<p>省略可能な文字列パラメーター。 WPP_CONTROL_GUIDS マクロが、指定したコントロールの GUID と名前付き 'Error'、'異常な' および 'ノイズ' WPP_DEFINE_BIT エントリを定義します。</p></td>
<td align="left">%(TraceWpp.WppAddControlGUID)</td>
<td align="left"><strong>-ctl:</strong><em>GUID</em></td>
</tr>
<tr class="even">
<td align="left"><strong>AdditionalOptions</strong>
<p>省略可能な文字列パラメーター。 コマンド ライン オプションの一覧。</p></td>
<td align="left">%(TraceWpp.WppAdditionalOptions)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>ConfigurationDirectories</strong>
<p>省略可能な string[] 型のパラメーター。 構成とテンプレート ファイルの場所を指定します。</p></td>
<td align="left">%(TraceWpp.WppConfigurationDirectories)</td>
<td align="left"><strong>-cfgdir:</strong><em>[パス]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>DllMacro</strong>
<p>省略可能なブール型パラメーター。 WPP_DLL マクロを定義します。</p></td>
<td align="left">%(TraceWpp.WppDllMacro)</td>
<td align="left"><strong>dll</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>FileExtensions</strong>
<p>省略可能な string[] 型のパラメーター。 ソース ファイルとして WPP を認識するファイルの種類を指定します。 WPP は、別のファイル名拡張子の付いたファイルを無視します。</p></td>
<td align="left">%(TraceWpp.WppFileExtensions)</td>
<td align="left"><strong>-ext:</strong><em>.ext1 [.ext2]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>IgnoreExclamationmarks</strong>
<p>省略可能なブール型パラメーター。 WPP '途切れ、' % などの複雑な書式設定で使用されるとも呼ばれる、感嘆符を無視するように指示! タイムスタンプ! % です。</p></td>
<td align="left">%(TraceWpp.WppIgnoreExclamationmarks)</td>
<td align="left"><strong>-noshrieks</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>Kernelmode であります。</strong>
<p>省略可能なブール型パラメーター。 カーネル モードのコンポーネントのトレース、WPP_KERNEL_MODE マクロを定義します。 既定では、ユーザー モード コンポーネントだけがトレースされます。</p></td>
<td align="left">%(TraceWpp.WppKernelMode)</td>
<td align="left"><strong>-km</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>OutputDirectory</strong>
<p>省略可能な文字列パラメーター。 WPP を作成する出力ファイルのディレクトリを指定します。</p></td>
<td align="left">%(TraceWpp.WppOutputDirectory)</td>
<td align="left"><strong>-odir:</strong><em>パス</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>PreprocessorDefinitions</strong>
<p>省略可能な string[] 型のパラメーター。 ソース ファイルの前処理シンボルを定義します。</p></td>
<td align="left">%(TraceWpp.WppPreprocessorDefinitions)</td>
<td align="left"><strong>/D</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>PreserveExtensions</strong>
<p>省略可能な string[] 型のパラメーター。 TMH ファイルを作成するときに、指定したファイル名拡張子が保持されます。</p></td>
<td align="left">%(TraceWpp.WppPreserveExtensions)</td>
<td align="left"><strong>-preserveext:</strong><em>ext1[,ext2]</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>ScanConfigurationData</strong>
<p>省略可能な文字列パラメーター。 カスタム データ型、および defaultwpp.ini では、構成ファイルではないファイルなど、構成データを検索します。</p></td>
<td align="left">%(TraceWpp.WppScanConfigurationData)</td>
<td align="left"><strong>-スキャン:</strong><em>ファイル</em></td>
</tr>
<tr class="even">
<td align="left"><strong>SearchString</strong>
<p>省略可能な文字列パラメーター。 WPP トレースを開始する指定した文字列のソース ファイルを検索するように指示します。</p></td>
<td align="left">%(TraceWpp.WppSearchString)</td>
<td align="left"><strong>-行末:</strong><em>文字列</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>ToolPath</strong>
<p>省略可能な文字列パラメーター。 ツールがあるフォルダーへの完全パスを指定することができます。</p></td>
<td align="left">$(WPPToolPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>トレース関数</strong>
<p>省略可能な string[] 型のパラメーター。 トレース メッセージを生成するために使用する関数を指定します。</p></td>
<td align="left">%(TraceWpp.WppTraceFunction)</td>
<td align="left"><strong>-func:</strong><em>FunctionDescription</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>省略可能な文字列パラメーター。 書き込む tlog の追跡ツールのログ ディレクトリ。</p></td>
<td align="left">%(TraceWpp.WppTrackerLogDirectory)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackFileAccess</strong>
<p>省略可能なブール型パラメーター。 True の場合は、このタスクのファイル アクセスのパターンを追跡します。</p></td>
<td align="left">$(TrackFileAccess)</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WPP プリプロセッサ](wpp-preprocessor.md)

[WPP ソフトウェア トレース](wpp-software-tracing.md)

 

 






