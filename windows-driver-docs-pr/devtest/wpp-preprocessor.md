---
title: WPP プリプロセッサ
description: WPP プリプロセッサ
ms.assetid: 92bcb2c4-f6de-4704-8f5c-9a2e5901616a
keywords:
- Windows ソフトウェア トレース プリプロセッサ WDK、オプション
- WDK、オプションのトレース WPP ソフトウェア
- WPP プリプロセッサ WDK
- Windows ソフトウェア トレース プリプロセッサ WDK、プリプロセッサを呼び出す
- WPP ソフトウェア トレース機能を WDK、プリプロセッサを呼び出す
- Windows ソフトウェア トレース プリプロセッサ WDK、ビルド プロセス
- WDK、ビルド プロセスのトレース WPP ソフトウェア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4b6bd50e9fb1cb992db8ef8399d4461ba96f985
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549008"
---
# <a name="wpp-preprocessor"></a>WPP プリプロセッサ


このセクションについて説明します、 *Windows ソフトウェア トレース プリプロセッサ*、WPP プリプロセッサとよく呼ばれます。

## <a name="span-idinvokingthewpppreprocessorspanspan-idinvokingthewpppreprocessorspan-invoking-the-wpp-preprocessor"></a><span id="invoking_the_wpp_preprocessor"></span><span id="INVOKING_THE_WPP_PREPROCESSOR"></span> WPP プリプロセッサを呼び出す


Visual Studio と MSBuild 環境を使用してプリプロセッサ WPP を呼び出すことができます。

**WPP プリプロセッサを呼び出す**

1.  ソリューション エクスプ ローラーでドライバーのプロジェクトを右クリックし、をクリックして**プロパティ。**
2.  プロジェクトのプロパティ ページで次のようにクリックします**構成プロパティ**クリック**WPP トレース。**
3.  **全般**設定、**実行 WPP**オプションを**はい**。
4.  **コマンドライン**トレースの動作をカスタマイズする以下のオプションを追加することができます。

    たとえば、 **WPP トレース**、1 つを指定する**構成データのスキャン**ファイル。

    カスタム データを指定する型のインスタンス、複数の 1 つの構成ファイルを提供する必要がある場合でファイルを参照**コマンドライン**を使用して、 **-スキャン**オプションなど。

    ```
    -scan:"$(KMDF_INC_PATH)\$(KMDF_VER_PATH)\WdfTraceEnums.h"
    ```

ビルド プロセスに関する詳細については、次を参照してください。 [TraceWPP タスク](tracewpp-task.md)と[WDK と Visual Studio ビルド環境](wdk-and-visual-studio-build-environment.md)します。

TraceWPP ツール (TraceWPP.exe) を使用して、ビルド環境から個別のプリプロセッサを実行することもできます。 このツールは、WDK の x86 bin サブディレクトリにあります。

## <a name="span-idwpptracinggeneraloptionsspanspan-idwpptracinggeneraloptionsspanspan-idwpptracinggeneraloptionsspanwpp-tracing-general-options"></a><span id="WPP_Tracing_General_Options"></span><span id="wpp_tracing_general_options"></span><span id="WPP_TRACING_GENERAL_OPTIONS"></span>WPP トレースの一般的なオプション


次の表では、WPP プリプロセッサのオプションについて説明します。 プロジェクトまたは TraceWPP ツールへのパラメーターとして、WPP トレースのプロパティ ページを使用して Visual Studio では、これらのオプションを構成できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP トレース オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WPP を実行します。</p></td>
<td align="left"><p>True の場合は、WPP を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>最小リビルドを有効にする</p></td>
<td align="left"><p>True の場合、追跡対象のインクリメンタル ビルドが実行されます。false の場合、再構築を実行します。</p></td>
</tr>
</tbody>
</table>

 

## <span id="run_wpp_options"></span><span id="RUN_WPP_OPTIONS"></span>


## <a name="span-idfunctionandmacrooptionsspanspan-idfunctionandmacrooptionsspanspan-idfunctionandmacrooptionsspanfunction-and-macro-options"></a><span id="Function_and_Macro_Options"></span><span id="function_and_macro_options"></span><span id="FUNCTION_AND_MACRO_OPTIONS"></span>関数とマクロのオプション


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP トレース オプション</th>
<th align="left">TraceWPP コマンド オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>プリプロセッサの定義</p></td>
<td align="left"><p><strong>-D</strong><em>マクロ</em></p></td>
<td align="left"><p>追加<strong>#定義</strong><em>マクロ</em>、生成されたファイルの先頭に、<em>マクロ</em>マクロの名前を指定します。</p>
<p>このオプションは、同じ効果として、 <strong>/D</strong> (マクロを定義する) コンパイラ オプション。 定義することを確認するには含まれる TMH ファイルの先頭には有効です。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p><strong>-D</strong><em>マクロ</em><strong>=</strong><em>拡張</em></p></td>
<td align="left"><p>追加<strong>#定義</strong><em>マクロの展開</em>、生成されたファイルの先頭に、<em>マクロ</em>マクロの名前を指定と<em>拡張</em>は展開されている値です。</p>
<p>このオプションは、同じ効果として、 <strong>/D</strong> (マクロを定義する) コンパイラ オプション。 定義することを確認するには含まれる TMH ファイルの先頭には有効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>カーネル モードのコンポーネントをトレースします。</p></td>
<td align="left"><p><strong>-km</strong></p></td>
<td align="left"><p>カーネル モードのコンポーネントのトレース、WPP_KERNEL_MODE マクロを定義します。 既定では、ユーザー モード コンポーネントだけがトレースされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Dll のマクロを有効にします。</p></td>
<td align="left"><p><strong>dll</strong></p></td>
<td align="left"><p>これにより WPP_INIT_TRACING が呼び出されるたびに初期化する WPP データ構造 WPP_DLL マクロを定義します。 それ以外の場合、構造体は、1 回だけ初期化されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>コントロールの GUID を指定します。</p></td>
<td align="left"><p><strong>-ctl:</strong><em>GUID</em></p></td>
<td align="left">定義、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556186" data-raw-source="[WPP_CONTROL_GUIDS](https://msdn.microsoft.com/library/windows/hardware/ff556186)">WPP_CONTROL_GUIDS</a>マクロを指定した<a href="control-guid.md" data-raw-source="[control GUID](control-guid.md)">コントロール GUID</a>および名前付きエラー、異常なおよびノイズ WPP_DEFINE_BIT エントリ。
<p>これは、ソース ファイルにマクロを追加する代わりにします。</p>
<p><em>GUID</em>コントロールの GUID を表します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsearchandformattingoptionsspanspan-idsearchandformattingoptionsspanspan-idsearchandformattingoptionsspansearch-and-formatting-options"></a><span id="Search_and_Formatting_Options"></span><span id="search_and_formatting_options"></span><span id="SEARCH_AND_FORMATTING_OPTIONS"></span>検索と書式設定オプション


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP トレース オプション</th>
<th align="left">TraceWPP コマンド オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>感嘆符を無視します。</p></td>
<td align="left"><p><strong>-noshrieks</strong></p></td>
<td align="left"><p>WPP とも呼ばれるの感嘆符を無視するように指示&quot;途切れします。&quot;</p>
<p>% などの複雑な書式設定に使用します。 タイムスタンプ! % です。 既定では、感嘆符が必要です、WPP がそれらを解釈しようとします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>数値書式指定文字列の番号付けの基本</p></td>
<td align="left"><p><strong>-argbase:</strong><em>数</em></p></td>
<td align="left"><p>などの書式指定文字列の番号付けの数値の基数を確立&quot;%1 %1!s!、%2!s! です。&quot;既定値は 1 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>トレース メッセージを生成するには、関数</p></td>
<td align="left"><p><strong>-func:</strong><em>FunctionDescription</em></p></td>
<td align="left"><p>代わる方法を指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff544918" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544918)"> <strong>DoTraceMessage</strong> </a>マクロ。 これらの関数は、トレース メッセージを生成し、使用できます。</p>
<p>たとえば、フラグと、トレース メッセージのレベルの両方をなどを指定する関数を定義できます。</p>
<pre space="preserve"><code>-func (DoMyTraceMessage(LEVEL,FLAGS,MSG,...)</code></pre>
<p>複数のインスタンスを使用することができます、 <strong>- func</strong>オプション。</p>
<p>このオプションは、ローカル構成ファイルで関数の説明を指定する代わりにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>検索する文字列を指定します。</p></td>
<td align="left"><p><strong>-行末:</strong><em>文字列</em></p></td>
<td align="left"><p>WPP トレースを開始する指定した文字列のソース ファイルを検索するように指示します。 既定では、WPP は文字列を検索&quot;WPP_INIT_TRACING します。&quot;</p>
<p>これは、ユーザーが独自のテンプレートを作成するための高度なオプションです。</p>
<p>たとえば、default.tpl: で</p>
<pre space="preserve"><code><code>IF FOUND WPP_INIT_TRACING</code>
 <code>INCLUDE um-init.tpl</code>
<code>ENDIF</code></code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p>モジュール名を指定します。</p></td>
<td align="left"><p><strong>-p: です。</strong><em>文字列</em></p></td>
<td align="left"><p>代替のフレンドリ名を指定します、 <a href="message-guid.md" data-raw-source="[message GUID](message-guid.md)">GUID をメッセージ</a>これからのメッセージの<a href="trace-provider.md" data-raw-source="[trace provider](trace-provider.md)">トレース プロバイダー</a>します。 既定では、メッセージの GUID のフレンドリ名は、トレース プロバイダーが構築されたディレクトリの名前です。</p>
<p>メッセージの GUID のフレンドリ名が表示されたら、既定で、<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">トレース メッセージのプレフィックス</a>、変数で表される<strong>%1</strong>します。 このパラメーターを使用するには、文字列、ユーザーが、トレース プロバイダー、トレース プロバイダーを含むモジュールの名前または重要度を作成して実装されているプロジェクトの名前のフレンドリ名など、トレース プロバイダーを識別するためにプレフィックスを追加するには段階上がってトレース プロバイダー。 この情報には、ユーザー別のファイルまたは別のパスに関連するトレース プロバイダーを関連付けることが役立ちます。</p>
<p><strong>-P</strong>パラメーターは、Windows Vista の Windows Driver Kit (WDK) に含まれている WPP のバージョン、および、WDK の以降のバージョンが必要です。 <strong>-P</strong>パラメーターは、Windows 2000 以降のバージョンの Windows で動作します。</p>
<p>例:</p>
<pre space="preserve"><code>-p:TraceDrv
-p:AudioModule</code></pre></td>
</tr>
</tbody>
</table>

 

## <a name="span-idfileoptionsspanspan-idfileoptionsspanspan-idfileoptionsspanfile-options"></a><span id="File_Options"></span><span id="file_options"></span><span id="FILE_OPTIONS"></span>ファイルのオプション


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP トレース オプション</th>
<th align="left">TraceWPP コマンド オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>追加のインクルード ディレクトリ</p></td>
<td align="left"><p><strong>-I</strong> <em>Path1</em><strong>[;</strong><em>Path2</em><strong>]</strong></p></td>
<td align="left"><p>インクルード パスに追加する 1 つまたは複数のディレクトリを指定します1 つ以上の場合、セミコロンで区切ります。 -として同じ<strong>cfgdir</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>構成ディレクトリ</p></td>
<td align="left"><p><strong>-cfgdir:</strong><em>Path1</em><strong>[;</strong><em>Path2</em><strong>]</strong></p></td>
<td align="left"><p>構成とテンプレート ファイルの場所を指定します。</p>
<p><em>Path1</em>と<em>Path2</em>ディレクトリへの完全修飾パスを表します。 複数のパスを指定することができます。 既定では、ローカル ディレクトリです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ファイル拡張子</p></td>
<td align="left"><p><strong>-ext: です。</strong> <em>ext1</em> <strong>[.</strong><em>ext2</em><strong>]</strong></p></td>
<td align="left"><p>ソース ファイルとして WPP を認識するファイルの種類を指定します。 WPP は、別のファイル名拡張子の付いたファイルを無視します。</p>
<p>既定では、WPP は .c、.c ファイルでは、.cpp と .cxx ファイルのみを認識します。</p>
<p>このオプションでは、WPP ではありませんがファイルを削除したり、リソースの名前を変更することがなく、WPP の既定の設定を使用できます。&#39;.rc、.mc ファイルなどを使用します。</p>
<p>たとえば、C++ ファイルとヘッダー (.h) ファイルには、トレースを追加するに次のコマンドを使用します。</p>
<p><strong>-ext:.cpp.CPP.h.H</strong></p>
<p>また、使用して、C++ とヘッダー ファイルの異なる名前 TMH ファイルを得られるように、 <strong>- preserveext</strong>オプション。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ファイルの拡張を維持します。</p></td>
<td align="left"><p><strong>-preserveext:</strong> <em>.ext1</em><strong>[.</strong><em>ext2</em><strong>]</strong></p></td>
<td align="left"><p>TMH ファイルを作成するときに、指定したファイル名拡張子が保持されます。</p>
<p>既定では、すべてのファイルの種類の TMH ファイルの名前は<em>filename</em>.tmh します。 これが原因ファイルは名前の競合と同じ名前の 1 つ以上のソース ファイルがある場合。</p>
<p>たとえば、既定では、C ファイル (.c) TMH ファイルとヘッダー (.h) ファイルは、するという名前&lt;filename&gt;.tmh します。 使用して<strong>- preserveext: .c .h</strong>、TMH ファイルの名前は&lt;filename&gt;. c.tmh と&lt;filename&gt;。 h.tmh。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>出力ディレクトリ</p></td>
<td align="left"><strong>-odir:</strong> <em>パス</em></td>
<td align="left"><p>WPP を作成する出力ファイルのディレクトリを指定します。</p>
<p><em>パス</em>ディレクトリへの完全修飾パスです。 既定では、ローカル ディレクトリです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>テンプレート ファイルを指定します</p></td>
<td align="left"><p><strong>-gen {File.tpl}<em>します。 ext</strong></p></td>
<td align="left"><p>中かっこの間で指定された名前の WPP を処理するすべてのソース ファイルの{}、指定したファイル名拡張子を持つ別のファイルを作成します。</p>
<p>File.tpl では、ソース ファイルを表します。 *.ext では、作成されるファイルとファイル名拡張子の種類を表します。</p>
<p>複数を指定する<strong>-gen</strong>オプション。</p>
<p>たとえば、 <strong>-gen {default.tpl の um}</em>.tmh</strong>あることを意味すべて<strong>um default.tpl</strong> WPP は次の処理、ファイルが生成されます、 <strong>um default.tmh</strong>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>構成データをスキャンします。</p></td>
<td align="left"><p><strong>-スキャン:</strong><em>ファイル</em></p></td>
<td align="left"><p>カスタム データ型、および defaultwpp.ini では、構成ファイルではないファイルなど、構成データを検索します。</p>
<p>場所<strong>begin_wpp config</strong>と<strong>end_wpp</strong>に関する構成データを識別する文字列。 Defaultwpp.ini で使用するために、構成データの同じ形式を使用します。</p>
<p>カスタム構成ファイルに構成データを追加した場合は、使用、 <strong>- ini</strong>パラメーター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>代替の構成ファイル</p></td>
<td align="left"><p><strong>-defwpp:</strong><em>パス</em></p></td>
<td align="left"><p>代替の構成ファイルを指定します。 Wpp は、defaultwpp.ini ファイルではなくこのファイルを使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>追加の構成ファイル</p></td>
<td align="left"><p><strong>-ini:</strong><em>パス</em></p></td>
<td align="left"><p>追加の構成ファイルを指定します。 WPP は、指定したファイルを使用して、既定のファイルだけでなく defaultwpp.ini します。</p>
<p>トレースの構成データを格納する新しい構成ファイルを作成したときに、このパラメーターを使用します。 構成データを別の種類のソースまたはヘッダー ファイルなどのファイルに追加した場合は、使用、 <strong>-スキャン</strong>パラメーター。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwppbuildprocessspanspan-idwppbuildprocessspanwpp-build-process"></a><span id="wpp_build_process"></span><span id="WPP_BUILD_PROCESS"></span>WPP ビルド プロセス


ドライバーまたはアプリケーション ファイルをコンパイルする前に、ドライバーまたはアプリケーションを構築 WPP がドライバーまたはユーザー モード アプリケーションの有効な場合に、WPP プリプロセッサを呼び出します。

WPP ビルド プロセスでは、次の手順を実行します。

1.  WPP プリプロセッサは、各ソース ファイルで WPP マクロを処理し、作成、[トレース メッセージのヘッダー ファイル](trace-message-header-file.md)ソース ファイルごとにします。 ソース コードは、直接変更されません。

2.  プリプロセッサ WPP 時に、トレース メッセージのヘッダー ファイルを作成した後が、C プリプロセッサは、通常の方法でのトレース メッセージのヘッダー ファイルに組み込まれている WPP マクロを処理します。

 

 





