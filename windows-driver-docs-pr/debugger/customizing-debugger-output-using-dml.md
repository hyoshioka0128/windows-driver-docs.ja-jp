---
title: DML を使用したデバッガー出力のカスタマイズ
description: デバッガーのマークアップ言語 (DML) は、デバッガーと拡張機能からの出力の強化メカニズムを提供します。
ms.assetid: 04984510-B95F-405F-81DF-E9D0673210B4
ms.date: 11/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: a734a7c41b28019e0b59fe63ba4a5120e9ed1527
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464164"
---
# <a name="customizing-debugger-output-using-dml"></a>DML を使用したデバッガー出力のカスタマイズ


デバッガーのマークアップ言語 (DML) は、デバッガーと拡張機能からの出力の強化メカニズムを提供します。 HTML と同様に、デバッガーのマークアップのサポートには、表示ディレクティブを追加、表示されない情報タグの形式で出力ができます。 WinDbg などのデバッガー ユーザー インターフェイスは、グリッドの表示など、情報の表示を拡張し、新しい動作を提供する DML で提供され、並べ替えの追加情報を解析します。 このトピックでは、DML を使用して、デバッグ出力をカスタマイズする方法について説明します。 有効化と DML での使用の概要については、デバッガーを参照してください[デバッガー マークアップ言語を使用して](debugger-markup-language-commands.md)します。

DML では、Windows 10 で使用でき、それ以降です。

## <a name="span-iddmloverviewspanspan-iddmloverviewspanspan-iddmloverviewspandml-overview"></a><span id="DML_Overview"></span><span id="dml_overview"></span><span id="DML_OVERVIEW"></span>DML の概要


上の DML のプライマリのデバッガーの出力に関連する情報にリンクする機能を提供する利点があります。 プライマリの DML タグの 1 つは、&lt;リンク&gt;のリンクからの出力に関連する情報にアクセスできることを示す、出力プロデューサーをタグには、アクションが記載されているします。 として、web ブラウザーで HTML リンクを含むこれにより、ユーザーにハイパーリンクが設定された情報を移動します。

ハイパーリンクが設定されたコンテンツを提供することの利点は、デバッガーとデバッガー拡張機能の検出性を強化するために使用できることです。 デバッガーとその拡張機能に、大量の機能が含まれているが、さまざまなシナリオで使用する適切なコマンドを決定することは難しい。 ユーザーは、どのようなコマンドは、特定のシナリオで使用できる単に知る必要があります。 ユーザーとカーネル デバッグの違いは、複雑さでさらに追加します。 多くの場合、つまり、多くのユーザーはデバッグ コマンドに役立てることができますを意識していません。 DML へのリンクは、わかりやすいテキスト、クリック可能なメニュー システム、またはリンクのヘルプなどの代替のプレゼンテーションでラップされる任意のデバッグ コマンドの機能を提供します。 DML を使用して、コマンドの出力は、手元のタスクに関連するその他の関連コマンドをユーザーに拡張できます。

**デバッガーの DML のサポート**

-   WinDbg でコマンド ウィンドウでは、すべての DML 動作をサポートし、色、フォント スタイル、およびリンクに表示されます。
-   – Ntsd、cdb および kd – コンソール デバッガーの色のモードが有効な場合は true。 コンソールで実行するときに DML、および、唯一のカラー属性のみサポートします。
-   リダイレクトされた I/O のデバッガー、ntsd – d または remote.exe セッションでは、色は表示されません。

## <a name="span-iddmlcontentspecificationspanspan-iddmlcontentspecificationspanspan-iddmlcontentspecificationspandml-content-specification"></a><span id="DML_Content_Specification"></span><span id="dml_content_specification"></span><span id="DML_CONTENT_SPECIFICATION"></span>DML コンテンツの指定


DML は、HTML などの完全なプレゼンテーション言語ではありません。 DML は意図的に非常に単純でごく少数のタグ。

リッチ テキストをサポートしていないすべてのデバッガー ツールためには、DML とプレーン テキスト間の単純な変換を許可する DML が設計されています。 これにより、DML が既存のデバッガー ツールのすべての関数にできます。 色などの効果は、それらを削除しても、実際の情報を伝送するテキストは削除されませんので簡単にサポートできます。

DML は、XML ではありません。 DML は、セマンティックも構造化情報を伝達しません。 前述のように、必要があります、単純なこのため、DML の DML とプレーン テキストの間でマッピング タグはすべて破棄します。

DML が拡張可能です。すべてのタグは事前定義されているし、既存のデバッガー ツールのすべてで機能するために検証します。

**タグの構造体**

XML と同様に、DML タグは、開始点として指定する、 &lt;tagname \[args\] &gt;し、次&lt;/tagname&gt;します。

**特殊文字**

DML のコンテンツには、特殊文字の XML や HTML の規則がほぼに従います。 文字 (&)、 &lt;、 &gt; "特別なとはプレーン テキストでは使用できません。 同等のエスケープされたバージョンは、&、 &lt;、&gt;と"。 たとえば文字列:

"Alice と Bob は、3 を考える&lt;4"

次の DML に変換されます。

```text
"Alice & Bob think 3 &lt 4"
```

**C プログラミング言語の書式設定文字**

XML や HTML から大きな出発ルール DML テキストが C 言語ストリーム スタイルの書式指定文字をプログラミングなどを含めることができますが\\b、 \\t、 \\r と\\n。 これは、デバッガーのテキストの既存の運用と使用量との互換性をサポートします。

## <a name="span-idexampledmlspanspan-idexampledmlspanspan-idexampledmlspanexample-dml"></a><span id="Example_DML"></span><span id="example_dml"></span><span id="EXAMPLE_DML"></span>DML の例


たとえば、ファイル c:\\Dml\_Experiment.txt には、次の行が含まれています。

```text
My DML Experiment
<link cmd="lmD musb*">List modules that begin with usb.</link>
```

次のコマンドは、コマンドのブラウザーのウィンドウで、テキストとリンクを表示します。

```dbgcmd
.browse .dml_start c:\Dml_Experiment.txt
```

![dml ファイル出力のスクリーン ショット](images/dmlcommands03.png)

クリックすると、 **usb で始まるモジュールを一覧表示**リンクでは、次の図のような出力を参照してください。

![モジュールの一覧のスクリーン ショット](images/dmlcommands04.png)

## <a name="span-idright-clickbehaviorindmlspanspan-idright-clickbehaviorindmlspanspan-idright-clickbehaviorindmlspanright-click-behavior-in-dml"></a><span id="Right-Click_Behavior_in_DML"></span><span id="right-click_behavior_in_dml"></span><span id="RIGHT-CLICK_BEHAVIOR_IN_DML"></span>DML での動作を右クリックします。


右クリックの動作は DML で使用できます。 このサンプルは、定義する方法を示しますを使用して動作を右クリックして&lt;altlink&gt;ブレークポイントを送信する[ **bp (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンドを送信、 [ **u (Unassemble)** ](u--unassemble-.md)正規表現をクリックします。

```text
<link cmd="u MyProgram!memcpy">
<altlink name="Set Breakpoint (bp)" cmd="bp MyProgram!memcpy" />
u MyProgram!memcpy
</link>
```

## <a name="span-iddmltagreferencespanspan-iddmltagreferencespanspan-iddmltagreferencespandml-tag-reference"></a><span id="DML_Tag_Reference"></span><span id="dml_tag_reference"></span><span id="DML_TAG_REFERENCE"></span>DML タグのリファレンス


### <a name="span-idlinkspanspan-idlinkspanltlinkgt"></a><span id="_link_"></span><span id="_LINK_"></span>&lt;リンク&gt;

*&lt;リンク\[名前 ="text"\] \[cmd ="デバッガー\_コマンド"\]\[alt =「ホバーを表示するテキスト」\] \[セクション ="name"\] &gt;リンク テキスト&lt;/link&gt;*

リンク タグは、DML で基本的なハイパー リンク メカニズムです。 クリック可能なリンクとしてリンク テキストを表示する DML プレゼンテーションをサポートするユーザー インターフェイスがよう指示します。 Cmd 仕様のリンクをクリックすると、デバッガー コマンドが実行され、その出力は、現在の出力を置き換える必要があります。

HTML のような名前付きのリンクの間を移動できるように、名前とセクションの引数&lt;名前&gt;と\#名前をサポートします。 UI のセクションの引数を持つリンクがクリックされたときは名前が一致するという名前のリンクをスキャンし、をスクロールして表示します。 これにより、同じページのさまざまなセクション (または新しいページの特定のセクション) を指すリンクできます。 DML のセクション名では、コマンド文字列の最後のセクション名ことを許可する新しい構文を定義することを回避するために別です。

プレーン テキストへの変換では、タグを削除します。

**例**

```text
<b> Handy Links </b>
<link cmd="!dml_proc">Display process information with DML rendering.</link>
<link cmd="kM">Display stack information with DML rendering.</link>
```

**例**

この例では、DML リンク上でマウス ポインターを移動するときに表示されるテキストを作成する alt 属性の使用を示します。

```text
<b>Hover Example</b>
<link cmd="lmD" alt="This link will run the list modules command and display the output in DML format">LmD</link>
```

### <a name="span-idaltlinkspanspan-idaltlinkspanltaltlinkgt"></a><span id="_altlink_"></span><span id="_ALTLINK_"></span>&lt;altlink&gt;

*&lt;altlink \[name=”text”\] \[cmd=”debugger\_command”\] \[section=”name”\]&gt;alt link text&lt;/altlink&gt;*

&lt;Altlink&gt;右クリックの動作は DML で使用可能なタグを提供します。 Cmd 仕様のリンクをクリックすると、デバッガー コマンドが実行され、その出力は、現在の出力を置き換える必要があります。 &lt;Altlink&gt;  タブと組み合わせるは通常、&lt;リンク&gt;タグを正規表現をサポートし、動作を右クリックします。

プレーン テキストへの変換では、タグを削除します。

**例**

この例では、定義を使用して動作を右クリックして&lt;altlink&gt;ブレークポイントを送信する[ **bp (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンドを送信、 [ **u (Unassemble)** ](u--unassemble-.md)正規表現をクリックします。

```text
<link cmd="u MyProgram!memcpy">
<altlink name="Set Breakpoint (bp)" cmd="bp MyProgram!memcpy" />
u MyProgram!memcpy
</link>
```

### <a name="span-idexecspanspan-idexecspanltexecgt"></a><span id="_exec_"></span><span id="_EXEC_"></span>&lt;exec&gt;

*&lt;exec cmd ="デバッガー\_コマンド"&gt;わかりやすいテキスト&lt;/exec&gt;*

Exec タグは、クリック可能な項目としてわかりやすいテキストを表示することでリンク タグに似ています。 ただし、コマンドのブラウザー ウィンドウで、exec タグを使用するときに、特定のコマンドは、現在の出力を置き換えることがなく実行が、このタグは、コマンドがメニューからのクリックで実行する方法を提供します。

プレーン テキストへの変換では、タグを削除します。

**例**

この例では、標準のクリックで 2 つのコマンドを定義する方法を示します。

```text
<b>Exec Sample</b>
<exec cmd="!dml_proc">Display process information with DML rendering.</exec>
<exec cmd="kM">Display stack information with DML rendering.</exec>
```

### <a name="span-idbspanspan-idbspanltbgt"></a><span id="_b_"></span><span id="_B_"></span>&lt;B&gt;

*&lt;b&gt;太字のテキスト&lt;/b&gt;*

このタグは、太字要求します。 &lt;B&gt;、&lt;は&gt;と&lt;u&gt;プロパティの混在環境に入れ子にすることができます。

プレーン テキストへの変換では、タグを削除します。

**例**

この例では、テキストを太字にする方法を示します。

```text
<b>This is bold Text</b>
```

### <a name="span-idispanspan-idispanltigt"></a><span id="_i_"></span><span id="_I_"></span>&lt;私&gt;

*&lt;&gt;テキストを斜体&lt;/i&gt;*

このタグは、斜体を要求します。 &lt;B&gt;、&lt;は&gt;と&lt;u&gt;プロパティの混在環境に入れ子にすることができます。

プレーン テキストへの変換では、タグを削除します。

**例**

この例では、テキストを斜体にする方法を示します。

```text
<i>This is italicized Text</i>
```

### <a name="span-iduspanspan-iduspanltugt"></a><span id="_u_"></span><span id="_U_"></span>&lt;U&gt;

*&lt;u&gt;underlined text&lt;/u&gt;*

このタグは、下線付きテキストを要求します。 &lt;B&gt;、&lt;は&gt;と&lt;u&gt;プロパティの混在環境に入れ子にすることができます。

プレーン テキストへの変換では、タグを削除します。

**例**

この例では、下線付きテキスト。

```text
<u>This is underlined Text</u>
```

**例**

この例では、太字、下線、およびテキストを斜体にするタグを結合する方法を示します。

```text
<b><u><i>This is bold, underlined and italizized text. </i></u></b> 
```

### <a name="span-idcolspanspan-idcolspanltcolgt"></a><span id="_col_"></span><span id="_COL_"></span>&lt;col&gt;

&lt;col fg="name" bg="name"&gt;text&lt;/col&gt;

テキストの前景色と背景の色を要求します。 色は、顧客を表示する色の種類を制御できるようにすると、絶対値ではなく、既知の色の名前として示されます。 (既定値は WinDbg にのみ適用されます) 現在の色の名前。

**前景色と背景要素タグ**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>設定</strong></td>
<td align="left"><strong>説明/例</strong></td>
</tr>
<tr class="even">
<td align="left"><p>wbg - Windows の背景</p>
<p>wfg - Windows の前景色</p></td>
<td align="left">既定のウィンドウの前景色および背景色。 既定のウィンドウとウィンドウのテキストのシステム カラーになります。
<p>&lt;col fg ="wfg"bg"wbg"=&gt;これは、標準の前景テキストをバック グラウンド/ &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>clbg - 現在の行の前景色</p>
<p>clfg - 現在の行の背景</p></td>
<td align="left">現在の行の背景色と前景色。 強調表示のシステム カラーを既定し、テキストを強調表示されます。
<p>&lt;col fg ="clfg"bg"clbg"=&gt;テスト テキスト - 現在の行&lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>empbg の強調表示されたバック グラウンド</p>
<p>emphfg - 強調フォア グラウンド</p></td>
<td align="left">強調表示されたテキスト。 薄い青に既定値です。
<p>&lt;col fg ="empfg"bg ="empbg"&gt;これは、強調の前景色および背景のテキスト&lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>subbg - バック グラウンドの末</p>
<p>subfg 末の前景色</p></td>
<td align="left">末のテキスト。 既定で非アクティブなキャプションのテキストと非アクティブなキャプションのシステム カラーです。
<p>&lt;col fg ="subfg"bg"subbg"=&gt;フォア グラウンドの末は、このテキストをバック グラウンド/ &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>normbg の通常のバック グラウンド</p>
<p>normfg の通常の前景色</p></td>
<td align="left">標準
<p>&lt;col fg ="normfg"bg"normbg"=&gt;テスト テキスト - Normal (normfg/normbg) &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>warnbg - バック グラウンドの警告</p>
<p>warnfg - 警告の前景色</p></td>
<td align="left">警告
<p>&lt;col fg ="warnfg"bg"warnbg"=&gt;テストのテキストの警告 (warnfg/warnbg) &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>errbg - エラーの背景</p>
<p>errfg - エラーの前景色</p></td>
<td align="left">[エラー]
<p>&lt;col fg ="errfg"bg"errbg"=&gt;テスト テキスト - エラー (errfg/errbg) &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>verbbg - 詳細な背景</p>
<p>verbfg - Verbose フォア グラウンド</p></td>
<td align="left">Verbose
<p>&lt;col fg="verbfg" bg="verbbg"&gt; Test Text - Verbose (verbfg / verbbg) &lt;/col&gt;</p></td>
</tr>
</tbody>
</table>



**ソース コードの 1 つの要素タグ**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>srcnum - ソース数値定数</p></td>
<td align="left">ソース要素の色。
<p>&lt;col fg="srcnum" bg="wbg"&gt; Test Text - srcnum &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcchar - ソース文字定数</p></td>
<td align="left"><p>&lt;col fg ="srcchar"bg"wbg"=&gt;テスト テキスト - srcchar &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srcstr - ソース文字列定数</p></td>
<td align="left"><p>&lt;col fg ="srcstr"bg"wbg"=&gt;テスト テキスト - srcstr &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcid-ソース識別子</p></td>
<td align="left"><p>&lt;col fg ="srcid"bg"wbg"=&gt;テスト テキスト - srcid &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srckw キーワード</p></td>
<td align="left"><p>&lt;col fg ="srckw"bg"wbg"=&gt;テスト テキスト - srckw &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcpair - ソースの中かっこまたは一致するシンボル ペア</p></td>
<td align="left"><p>&lt;col fg ="srcpair"bg"empbbg"=&gt;テスト テキスト - srcpair &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srccmnt - ソースのコメント</p></td>
<td align="left"><p>&lt;col fg ="srccmnt"bg"wbg"=&gt;テスト テキスト - srccmnt &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcdrct - ソース ディレクティブ</p></td>
<td align="left"><p>&lt;col fg ="srcdrct"bg"wbg"=&gt;テスト テキスト - srcdrct &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srcspid - ソースの特殊な識別子</p></td>
<td align="left"><p>&lt;col fg ="srcspid"bg"wbg"=&gt;テスト テキスト - srcspid &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcannot - ソースの注釈</p></td>
<td align="left"><p>&lt;col fg ="srcannot"bg"wbg"=&gt;テスト テキスト - srcannot &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>変更されたデータを変更</p></td>
<td align="left">WinDbg で変更されたレジスタなど、以前の停止時点以降に変更されたデータに使用します。 既定値は赤です。
<p>&lt;col fg =「変更」bg"wbg"=&gt;テスト テキスト - 変更&lt;/col&gt;</p></td>
</tr>
</tbody>
</table>



## <a name="span-iddmlexamplecodespanspan-iddmlexamplecodespanspan-iddmlexamplecodespandml-example-code"></a><span id="DML_Example_Code"></span><span id="dml_example_code"></span><span id="DML_EXAMPLE_CODE"></span>DML のコード例


次のコード例を示しています。

-   デバッグ コマンドを呼び出す
-   コマンドを右クリックを実装します。
-   テキストの上のポイントを実装します。
-   色とリッチ テキストを使用します。

```XML
<col fg="srckw" bg="wbg"> <b>
*******************************************************
*** Example debug commands for crash dump analysis ****
*******************************************************
</b></col>
<col fg="srcchar" bg="wbg"><i>
**** Hover over commands for additional information ****
        **** Right-click for command help ****
</i></col>

<col fg="srccmnt" bg="wbg"><b>*** Common First Steps for Crash Dump Analysis ***</b> </col>
<link cmd=".symfix" alt="Set standard symbol path using .symfix">.symfix<altlink name="Help about .symfix" cmd=".hh .symfix" /> </link> - Set standard symbol path
<link cmd=".sympath+ C:\Symbols" alt="This link adds addtional symbol directories">.sympath+ C:\Symbols<altlink name="Help for .sympath" cmd=".hh .sympath" /> </link> - Add any additional symbol directories, for example C:\Symbols
<link cmd=".reload /f" alt="This link reloads symbols">.reload /f<altlink name="Help for .reload" cmd=".hh .reload" /> </link> - Reloads symbols to make sure they are in good shape
<link cmd="!analyze -v" alt="This link runs !analyze with the verbose option">!analyze -v<altlink name="Help for !analyze" cmd=".hh !analyze" /> </link> - Run !analyze with the verbose option
<link cmd="vertarget" alt="This link runs checks the target version">vertarget<altlink name="Help for vertarget" cmd=".hh vertarget" /></link> - Check the target version
<link cmd="version" alt="This link displays the versions in use">version<altlink name="Help for version" cmd=".hh version" /></link> - Display the versions in use
<link cmd=".chain /D" alt="This link runs .chain">.chain /D<altlink name="Help for .chain" cmd=".hh .chain" /></link> - Use the .chain /D command to list debugger extensions
<link cmd="kM" alt="This link displays the stack backtrace using DML">kD<altlink name="Help for k" cmd=".hh k, kb, kc, kd, kp, kP, kv (Display Stack Backtrace)" /> </link> - Display the stack backtrace using DML rendering
<link cmd="lmD" alt="This link will run the list modules command and display the output in DML format">LmD<altlink name="Help for lmD" cmd=".hh lm" /> </link> - List modules command and display the output in DML format
<link cmd=".help /D" alt="Display help for commands">.help /D <altlink name="Help for .dot commands" cmd=".hh commands" /></link> - Display help for commands in WinDbg
<link cmd=".hh" alt="Start help">.hh<altlink name="Debugger Reference Help".hh Contents" cmd=".hh Debugger Reference" /></link> - Start help

<col fg="srccmnt" bg="wbg"><b>*** Registers and Context ***</b></col>
<link cmd="r" alt="This link displays registers">r<altlink name="Help about r command" cmd=".hh r" /></link>  - Display registers
<link cmd="dt nt!_CONTEXT" alt="This link displays information about nt_CONTEXT">dt nt!_CONTEXT<altlink name="Help about the dt command" cmd=".hh dt" /></link> - Display information about nt_CONTEXT
<link cmd="dt nt!_PEB" alt="This link calls the dt command to display nt!_PEB">dt nt!_PEB<altlink name="Help about dt command" cmd=".hh dt" /></link> - Display information about the nt!_PEB
<link cmd="ub" alt="This link unassembles backwards">ub<altlink name="Help about ub command" cmd=".hh u, ub, uu (Unassemble)" /></link> - Unassemble Backwards

<col fg="srcchar" bg="wbg"><i>
**** Note: Not all of the following commands will work with all crash dump data ****
</i></col>
<col fg="srccmnt" bg="wbg"><b>*** Device Drivers ***</b></col>
<link cmd="!devnode 0 1" alt="This link displays the devnodes">!devnode 0 1<altlink name="Help about !devnode command" cmd=".hh !devnode" /></link> - Display devnodes
<link cmd=".load wdfkd.dll;!wdfkd.help" alt="Load wdfkd extensions and display help">.load wdfkd.dll;!wdfkd.help<altlink name="Help about the wdfkd extensions" cmd=".hh !wdfkd" /></link> - Load wdfkd extensions and display help
<link cmd="!wdfkd.wdfldr" alt="This link displays !wdfkd.wdfldr">!wdfkd.wdfldr<altlink name="Help about !wdfkd.wdfldr" cmd=".hh !wdfkd.wdfldr" /></link>  - Display WDF framework driver loader information
<link cmd="!wdfkd.wdfumtriage" alt="This link displays !wdfkd.umtriage">!wdfkd.umtriage<altlink name="Help about !wdfkd.umtriage" cmd=".hh !wdfkd_wdfumtriage" /></link> - Display WDF umtriage driver information

<col fg="srccmnt" bg="wbg"><b>*** IRPs and IRQL ***</b></col>
<link cmd="!processirps" alt="This link displays process IRPs">!processirps<altlink name="Help about !processirps command" cmd=".hh !processirps" /></link> - Display process IRPs
<link cmd="!irql" alt="This link displays !irql">!irql<altlink name="Help about !irql command" cmd=".hh !irql" /></link> - Run !irql

<col fg="srccmnt" bg="wbg"><b>*** Variables and Symbols ***</b></col>
<link cmd="dv" alt="This link calls the dv command">dv<altlink name="Help about dv command" cmd=".hh dv" /></link> - Display the names and values of all local variables in the current scope

<col fg="srccmnt" bg="wbg"><b>*** Threads, Processes, and Stacks ***</b></col>
<link cmd="!threads" alt="This link displays threads">!threads<altlink name="Help about the !threads command" cmd=".hh !threads" /></link> - Display threads
<link cmd="!ready 0xF" alt="This link runs !ready 0xF">!ready 0xF<altlink name="Help about the !ready command" cmd=".hh !ready" /></link> - Display threads in the ready state
<link cmd="!process 0 F" alt="This link runs !process 0 F ">!process 0 F<altlink name="Help about the !process command" cmd=".hh !process" /></link> - Run !process 0 F
<link cmd="!stacks 2" alt="This link displays stack information using !stacks 2 ">!stacks 2<altlink name="Help about the !stacks command" cmd=".hh !stacks" /></link> - Display stack information using !stacks 2
<link cmd=".tlist" alt="This link displays a process list using TList ">tlist<altlink name="Help about the TList command" cmd=".hh .tlist" /></link> - Display a process list using tlist
<link cmd="!process" alt="This link displays process ">!process<altlink name="Help about the !process command" cmd=".hh !process" /></link> - Display process information
<link cmd="!dml_proc" alt="This link displays process information with DML rendering.">!dml_proc<altlink name="Help about the !dml_proc command" cmd=".hh !dml_proc" /></link> - Display process information with DML rendering
```

このコード例では、色と書式設定タグの使用方法を示します。

```XML
*** Text Tag Examples ****

<b>This is bold text</b>
<u>This is underlined text</u>
<i>This is italizized text</i>
<b><u><i>This is bold, underlined and italizized text</i></u></b>

<b>Color Tag Examples</b>
<col fg="wfg" bg="wbg"> This is standard foreground / background text </col>
<col fg="empfg" bg="empbg"> This is emphasis foreground / background text </col>
<col fg="subfg" bg="subbg"> This is subdued foreground / background text </col>
<col fg="clfg" bg="clbg"> Test Text - Current Line</col>

<b>Other Tags Sets</b>
<col fg="normfg" bg="normbg"> Test Text - Normal (normfg / normbg) </col>
<col fg="warnfg" bg="warnbg"> Test Text - Warning (warnfg / warnbg) </col>
<col fg="errfg" bg="errbg"> Test Text - Error (errfg / errbg) </col>
<col fg="verbfg" bg="verbbg"> Test Text - Verbose (verbfg / verbbg) </col>

<b>Changed Text Tag Examples</b>
<col fg="changed" bg="wbg"> Test Text - Changed</col>

<b>Source Tags - using wbg background</b>
<col fg="srcnum" bg="wbg"> Test Text - srcnum  </col>
<col fg="srcchar" bg="wbg"> Test Text - srcchar  </col>
<col fg="srcstr" bg="wbg"> Test Text - srcstr  </col>
<col fg="srcid " bg="wbg"> Test Text - srcid   </col>
<col fg="srckw" bg="wbg"> Test Text - srckw </col>
<col fg="srcpair" bg="empbbg"> Test Text - srcpair </col>
<col fg="srccmnt" bg="wbg"> Test Text - srccmnt  </col>
<col fg="srcdrct" bg="wbg"> Test Text - srcdrct </col>
<col fg="srcspid" bg="wbg"> Test Text - srcspid </col>
<col fg="srcannot" bg="wbg"> Test Text - srcannot </col>

<b>Source Tags - using empbg background</b>
<col fg="srcnum" bg="empbg"> Test Text - srcnum  </col>
<col fg="srcchar" bg="empbg"> Test Text - srcchar  </col>
<col fg="srcstr" bg="empbg"> Test Text - srcstr  </col>
<col fg="srcid " bg="empbg"> Test Text - srcid   </col>
<col fg="srckw" bg="empbg"> Test Text - srckw </col>
<col fg="srcpair" bg="empbbg"> Test Text - srcpair </col>
<col fg="srccmnt" bg="empbg"> Test Text - srccmnt  </col>
<col fg="srcdrct" bg="empbg"> Test Text - srcdrct </col>
<col fg="srcspid" bg="empbg"> Test Text - srcspid </col>
<col fg="srcannot" bg="empbg"> Test Text - srcannot </col>

<b>Source Tags - using subbg background</b>
<col fg="srcnum" bg="subbg"> Test Text - srcnum  </col>
<col fg="srcchar" bg="subbg"> Test Text - srcchar  </col>
<col fg="srcstr" bg="subbg"> Test Text - srcstr  </col>
<col fg="srcid " bg="subbg"> Test Text - srcid   </col>
<col fg="srckw" bg="subbg"> Test Text - srckw </col>
<col fg="srcpair" bg="subbg"> Test Text - srcpair </col>
<col fg="srccmnt" bg="subbg"> Test Text - srccmnt  </col>
<col fg="srcdrct" bg="subbg"> Test Text - srcdrct </col>
<col fg="srcspid" bg="subbg"> Test Text - srcspid </col>
<col fg="srcannot" bg="subbg"> Test Text - srcannot </col>
```

## <a name="span-iddmladditionstothedbgenginterfacespanspan-iddmladditionstothedbgenginterfacespanspan-iddmladditionstothedbgenginterfacespandml-additions-to-the-dbgeng-interface"></a><span id="DML_Additions_to_the_dbgeng_Interface"></span><span id="dml_additions_to_the_dbgeng_interface"></span><span id="DML_ADDITIONS_TO_THE_DBGENG_INTERFACE"></span>DML dbgeng インターフェイスの追加


[デバッガー エンジンと拡張機能 Api](debugger-engine-and-extension-apis.md)デバッガー エンジンを使用して、カスタム アプリケーションを作成するインターフェイスを提供します。 WinDbg、KD、CDB、NTSD で実行されるカスタムの拡張機能を記述することもできます。 詳細については、次を参照してください。 [DbgEng 拡張機能の作成](writing-dbgeng-extensions.md)です。 このセクションでは、デバッガー エンジンのインターフェイスを使用できる DML 拡張機能について説明します。

一連のテキスト処理の入力メソッドとインターフェイスの出力に、dbgeng は既に、DML の使用には、入力と出力のテキストに含まれるコンテンツの種類の指定のみが必要です。

**Dbgeng に DML のコンテンツを提供します。**

出力制御フラグ デバッグ\_OUTCTL\_DML では、dbgeng メソッドによって生成されたテキストが DML コンテンツとして処理することを示します。 このフラグを指定しない場合、テキストはプレーン テキストのコンテキストとして扱われます。 デバッグ\_OUTCTL\_DML は、次の方法で使用できます。

-   [**IDebugControl4::ControlledOutput**](https://msdn.microsoft.com/library/windows/hardware/ff539248)
-   [**IDebugControl4::ControlledOutputVaList**](https://msdn.microsoft.com/library/windows/hardware/ff539252)
-   [**IDebugControl4::ControlledOutputWide**](https://msdn.microsoft.com/library/windows/hardware/ff539266)
-   [**IDebugControl4::ControlledOutputVaListWide**](https://msdn.microsoft.com/library/windows/hardware/ff539259)

指定されたテキストは、有効な文字 DML 規則に従う必要があります。

新しい書式指定子 % を許可するすべての出力ルーチンが強化されています\[h | w\]Y {t} します。 この書式指定子は、引数として文字列ポインターを備え、指定されたテキストがプレーン テキストであり、出力の処理中に DML 形式に変換する必要があることを示します。 これにより、呼び出し元は DML コンテンツに変換しなくても事前 DML 形式自体などのプレーン テキストの簡単な方法です。 H、w の修飾子は、%s と同様、ANSI または Unicode 文字を示します。

次の表では、%Y 書式指定子の使用を示します。

|        |                                                                                                                                                                                                                                    |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| %Y {t}  | 引用符で囲まれた文字列。 テキストは、出力形式の場合、DML に変換されます (最初の引数) は、DML します。                                                                                                                                                   |
| %Y {T}  | 引用符で囲まれた文字列。 常にテキストに変換する DML 出力形式に関係なく。                                                                                                                                                    |
| %Y {s}  | 引用符なしの文字列。 テキストは、出力形式の場合、DML に変換されます (最初の引数) は、DML します。                                                                                                                                                 |
| %Y {S}  | 引用符なしの文字列。 常にテキストに変換する DML 出力形式に関係なく。                                                                                                                                                  |
| %Y {、} | ULONG64. 空の文字列またはポインター フィールドを書式設定されたデバッガーの上位 32 ビット部のパディングの間隔の 9 文字のいずれかを追加します。 余分なスペースは、上限の 8 ゼロが含まれていますを 9 スペースに出力だけでなく、\`文字。 |
| %Y {ps} | ULONG64. 埋め込みのデバッガーの余分なスペースがポインターのフィールドを書式設定 (上位 8 ゼロが含まれていますだけでなく、\`文字)。                                                                                                             |
| %Y {l}  | ULONG64. 行情報のソースとしてのアドレスします。                                                                                                                                                                                       |



このコード スニペットでは、%Y 書式指定子の使用方法を示します。

```cpp
HRESULT CALLBACK testout(_In_ PDEBUG_CLIENT pClient, _In_ PCWSTR /*pwszArgs*/)
{
    HRESULT hr = S_OK;

    ComPtr<IDebugControl4> spControl;
    IfFailedReturn(pClient->QueryInterface(IID_PPV_ARGS(&spControl)));

    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{t}: %Y{t}\n", L"Hello <World>");
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{T}: %Y{T}\n", L"Hello <World>");
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{s}: %Y{s}\n", L"Hello <World>");
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{S}: %Y{S}\n", L"Hello <World>");

    spControl->ControlledOutputWide(0, DEBUG_OUTPUT_NORMAL, L"TEXT/NORMAL Y{t}: %Y{t}\n", L"Hello <World>");
    spControl->ControlledOutputWide(0, DEBUG_OUTPUT_NORMAL, L"TEXT/NORMAL Y{T}: %Y{T}\n", L"Hello <World>");
    spControl->ControlledOutputWide(0, DEBUG_OUTPUT_NORMAL, L"TEXT/NORMAL Y{s}: %Y{s}\n", L"Hello <World>");
    spControl->ControlledOutputWide(0, DEBUG_OUTPUT_NORMAL, L"TEXT/NORMAL Y{S}: %Y{S}\n", L"Hello <World>");

    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{a}: %Y{a}\n", (ULONG64)0x00007ffa7da163c0);
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{as} 64bit   : '%Y{as}'\n", (ULONG64)0x00007ffa7da163c0);
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{as} 32value : '%Y{as}'\n", (ULONG64)0x1);

    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{ps} 64bit   : '%Y{ps}'\n", (ULONG64)0x00007ffa7da163c0);
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{ps} 32value : '%Y{ps}'\n", (ULONG64)0x1);

    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{l}: %Y{l}\n", (ULONG64)0x00007ffa7da163c0);

    return hr;

}
```

このサンプル コードでは、次の出力を生成します。

```dbgcmd
0:004> !testout
DML/NORMAL Y{t}: "Hello <World>"
DML/NORMAL Y{T}: "Hello <World>"
DML/NORMAL Y{s}: Hello <World>
DML/NORMAL Y{S}: Hello <World>
TEXT/NORMAL Y{t}: "Hello <World>"
TEXT/NORMAL Y{T}: "Hello &lt;World&gt;"
TEXT/NORMAL Y{s}: Hello <World>
TEXT/NORMAL Y{S}: Hello &lt;World&gt;
DML/NORMAL Y{a}: 00007ffa`7da163c0
DML/NORMAL Y{as} 64bit   : '         '
DML/NORMAL Y{as} 32value : '         '
DML/NORMAL Y{ps} 64bit   : '        '
DML/NORMAL Y{ps} 32value : '        '
DML/NORMAL Y{l}: [d:\th\minkernel\kernelbase\debug.c @ 443]
```

デバッグ、さらに制御フラグ\_OUTCTL\_アンビエント\_DML、out 出力コントロールの属性を変更することがなく DML コンテキストのテキストを指定をできるようにします。 デバッグ\_OUTCTL\_アンビエント\_テキストが追加されましたもわかりやすいエイリアスとして以前から存在してデバッグ\_OUTCTL\_アンビエントです。 出力の制御フラグは、dbgeng.h で定義されます。

```cpp
#define DEBUG_OUTCTL_DML               0x00000020

// Special values which mean leave the output settings
// unchanged.
#define DEBUG_OUTCTL_AMBIENT_DML       0xfffffffe
#define DEBUG_OUTCTL_AMBIENT_TEXT      0xffffffff

// Old ambient flag which maps to text.
#define DEBUG_OUTCTL_AMBIENT           DEBUG_OUTCTL_AMBIENT_TEXT
```

**デバッグ対象から DML のコンテンツを提供します。**

されましたが、dbgeng – 特別なマーカーのデバッグ出力をスキャンするように強化 – デバッグ対象の出力の一部では、残りのテキストは、DML として扱うかを示します。 のみモードの変更は、1 つの 1 つの OutputDebugString 文字列などのデバッグ対象の出力に適用され、グローバル モードの切り替えではありません。

この例では、さまざまな形式、および DML の出力を示します。

```text
OutputDebugString(“This is plain text\n<?dml?>This is <col fg=\”emphfg\”>DML</col> text\n”);
```

生成された出力で、プレーン テキストが続く DML DML 頭字語が異なる色で表示される場所の行の行になります。

**IDebugOutputCallbacks2**

IDebugOutputCallbacks2 は、dbgeng プレゼンテーションの完全な DML コンテンツを受信するインターフェイスのクライアントを使用できます。 既存の SetOutputCallbacks メソッドに渡すことができるように、IDebugOutputCallbacks2、IDebugOutputCallbacks (IDebugOutputCallbacksWide されません) の拡張です。 エンジンは、着信出力コールバック オブジェクト サポート インターフェイスを表示する IDebugOutputCallbacks2 の QueryInterface を実行します。 IDebugOutputCallbacks2; IDebugOutputCallbacks2 の拡張メソッドを通じてすべての出力が送信されますが、オブジェクトにサポートしている場合基本的な IDebugOutputCallbacks::Output メソッドは使用されません。

新しいメソッドは次のとおりです。

-   IDebugOutputCallbacks2::GetInterestMask – により、受信する通知の出力の種類を記述するコールバック オブジェクトです。 プレーン テキスト コンテンツの間で基本的な選択では (デバッグ\_OUTCBI\_テキスト) と DML コンテンツ (デバッグ\_OUTCBI\_DML)。 さらに、コールバック オブジェクトには通知を明示的なフラッシュが要求するも (デバッグ\_OUTCBI\_EXPLICIT\_フラッシュ)。
-   IDebugOutputCallbacks2::Output2 – Output2 いきます IDebugOutputCallbacks2 のすべての通知。 パラメーターは、どのような種類の通知フラグ中に予定されていることを示します、Arg とテキストのパラメーターは、通知ペイロードを送信します。 通知は次のとおりです。

    -   デバッグ\_OUTCB\_テキスト-プレーン テキストを出力します。 フラグは、デバッグから\_OUTCBF\_\*Arg が出力マスクおよびテキストはプレーン テキスト。 場合はこの受信のみデバッグ\_OUTCBI\_関心マスク内のテキストが指定されました。

    -   デバッグ\_OUTCB\_DML – DML コンテンツ出力します。 フラグは、デバッグから\_OUTCBF\_\*Arg が出力マスクし、テキスト、DML コンテンツ。 場合はこの受信のみデバッグ\_OUTCBI\_関心マスクで DML が指定されました。
    
    -   デバッグ\_OUTCB\_EXPLICIT\_フラッシュ: 呼び出し元がという FlushCallbacks バッファー内のテキストがありません。 バッファー内のテキストがフラッシュされるときに通常どおりデバッグ\_OUTCBF\_COMBINED\_EXPLICIT\_を 1 つに 2 つの通知を折りたたみ、フラッシュのフラグが設定されます。 テキストがバッファリングされることはない場合、フラッシュのみ通知が送信されます。

 目的のマスク フラグは、次に示すように、dbgeng.h で定義されます。

 ```cpp
 // IDebugOutputCallbacks2 interest mask flags.
 //
 // Indicates that the callback wants notifications
// of all explicit flushes.
#define DEBUG_OUTCBI_EXPLICIT_FLUSH 0x00000001
// Indicates that the callback wants
// content in text form.
#define DEBUG_OUTCBI_TEXT           0x00000002
// Indicates that the callback wants
// content in markup form.
#define DEBUG_OUTCBI_DML            0x00000004

#define DEBUG_OUTCBI_ANY_FORMAT     0x00000006
 ```

その両方を処理できる場合に、テキストと DML コンテンツの出力オブジェクトを登録できますに注意してください。 出力は、エンジンを取得するコールバックを処理中に形式変換、つまり両方をサポートしているを削減するは、エンジンで変換を減らすことができます。 ただしではありません、必要に応じて、および操作の必要なモードは、1 つだけの形式をサポートします。

**自動変換**

Dbgeng は必要に応じて、プレーン テキストと DML の間に自動的に変換します。 など、エンジンに、呼び出し元がコンテンツにある DML を送信する場合、エンジンに変換プレーン テキスト プレーン テキストのみを許可するすべての出力クライアント。 代わりに、エンジン プレーン テキストに変換する DML をのみ DML を受け入れるすべての出力のコールバック。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバッガーのマークアップ言語を使用してください。](debugger-markup-language-commands.md)










