---
title: DML を使用したデバッガー出力のカスタマイズ
description: デバッガーマークアップ言語 (DML) は、デバッガーと拡張機能からの出力を拡張するための機構を提供します。
ms.assetid: 04984510-B95F-405F-81DF-E9D0673210B4
ms.date: 11/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: d0524a0bed0dbea8f4433c82983726961af28c42
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968051"
---
# <a name="customizing-debugger-output-using-dml"></a>DML を使用したデバッガー出力のカスタマイズ


デバッガーマークアップ言語 (DML) は、デバッガーと拡張機能からの出力を拡張するための機構を提供します。 HTML と同様に、デバッガーのマークアップサポートにより、出力には、表示ディレクティブや追加の非表示情報をタグの形式で含めることができます。 WinDbg などのデバッガーユーザーインターフェイスは、情報の表示を強化し、グリッドの表示や並べ替えなどの新しい動作を提供するために、DML に用意されている追加情報を解析します。 このトピックでは、DML を使用してデバッグ出力をカスタマイズする方法について説明します。 デバッガーでの DML の有効化と使用に関する一般的な情報については、「[デバッガーマークアップ言語の使用](debugger-markup-language-commands.md)」を参照してください。

DML は、Windows 10 以降で使用できます。

## <a name="span-iddml_overviewspanspan-iddml_overviewspanspan-iddml_overviewspandml-overview"></a><span id="DML_Overview"></span><span id="dml_overview"></span><span id="DML_OVERVIEW"></span>DML の概要


DML の主な利点は、デバッガーの出力の関連情報にリンクする機能を提供することです。 プライマリ DML タグの1つは &lt; link &gt; タグです。これにより、出力プロデューサーは、出力に関連する情報に、リンクの記述されたアクションを通じてアクセスできることを示します。 Web ブラウザーの HTML リンクと同様に、これにより、ハイパーリンクされた情報をユーザーがナビゲートできるようになります。

ハイパーリンクコンテンツを提供する利点は、デバッガーとデバッガー拡張機能の検出性を高めるために使用できることです。 デバッガーとその拡張機能には多くの機能が含まれていますが、さまざまなシナリオで使用する適切なコマンドを決定するのは困難な場合があります。 ユーザーは、特定のシナリオで使用できるコマンドを把握している必要があります。 ユーザーとカーネルのデバッグの違いにより、複雑さが増します。 これは多くの場合、多くのユーザーがデバッグコマンドを認識しないため、役に立ちます。 DML リンクを使用すると、テキストの説明、クリック可能なメニューシステム、リンクされたヘルプなど、任意のデバッグコマンドを別のプレゼンテーションにラップすることができます。 DML を使用すると、コマンドの出力を拡張して、タスクに関連する追加の関連コマンドをユーザーに案内することができます。

**デバッガーの DML サポート**

-   WinDbg のコマンドウィンドウでは、すべての DML 動作がサポートされており、色、フォントスタイル、およびリンクが表示されます。
-   コンソールデバッガー– ntsd、cdb、および kd –は、DML の色属性のみをサポートし、色モードが有効になっている真のコンソールで実行する場合にのみサポートします。
-   リダイレクトされた i/o、ntsd – d、または remote.exe セッションを使用したデバッガーでは、色は表示されません。

## <a name="span-iddml_content_specificationspanspan-iddml_content_specificationspanspan-iddml_content_specificationspandml-content-specification"></a><span id="DML_Content_Specification"></span><span id="dml_content_specification"></span><span id="DML_CONTENT_SPECIFICATION"></span>DML コンテンツの仕様


DML は、HTML などの完全なプレゼンテーション言語としては意図されていません。 DML は意図的に非常に単純であり、いくつかのタグだけが含まれています。

すべてのデバッガーツールがリッチテキストをサポートしているわけではないため、dml は DML とプレーンテキスト間の単純な変換を可能にするように設計されています。 これにより、DML をすべての既存のデバッガーツールで機能させることができます。 色などの効果は、それらを削除しても、実際の情報を保持するテキストは削除されないため、簡単にサポートできます。

DML は XML ではありません。 DML では、セマンティックおよび構造化された情報を実行しません。 前述のように、DML とプレーンテキストの間には単純なマッピングが必要です。このため、DML タグはすべて破棄可能です。

DML は拡張できません。すべてのタグが事前に定義され、すべての既存のデバッガーツールで動作するように検証されます。

**タグ構造**

XML と同様に、DML タグは、開始タグ &lt; \[ 引数 \] &gt; と次の &lt; /tagname と &gt; して指定されます。

**特殊文字**

DML コンテンツは、特殊文字の XML/HTML ルールにおおよそ従います。 、、および & 文字は &lt; &gt; 特殊で、プレーンテキストでは使用できません。 同じエスケープバージョンは、、 &lt; 、 &gt; および & ます。 次に例を示します。

"Alice & Bob は 3 4 と考えています &lt; "

は、次の DML に変換されます。

```text
"Alice & Bob think 3 &lt 4"
```

**C プログラミング言語の書式設定文字**

XML/HTML ルールから大きな出発点として、DML テキストには \\ 、b、 \\ t、 \\ r、n などの C プログラミング言語のストリームスタイルの書式設定文字を含めることができ \\ ます。 これは、既存のデバッガーテキストの実稼働と使用との互換性をサポートするためのものです。

## <a name="span-idexample_dmlspanspan-idexample_dmlspanspan-idexample_dmlspanexample-dml"></a><span id="Example_DML"></span><span id="example_dml"></span><span id="EXAMPLE_DML"></span>DML の例


ファイル C: \\ DmlExperiment.txt に \_ 次の行が含まれているとします。

```text
My DML Experiment
<link cmd="lmD musb*">List modules that begin with usb.</link>
```

次のコマンドを実行すると、テキストとリンクがコマンドブラウザーウィンドウに表示されます。

```dbgcmd
.browse .dml_start c:\Dml_Experiment.txt
```

![dml ファイル出力のスクリーンショット](images/dmlcommands03.png)

[ **Usb リンクで始まるモジュールの一覧**] をクリックすると、次の図のような出力が表示されます。

![モジュール一覧のスクリーンショット](images/dmlcommands04.png)

## <a name="span-idright-click_behavior_in_dmlspanspan-idright-click_behavior_in_dmlspanspan-idright-click_behavior_in_dmlspanright-click-behavior-in-dml"></a><span id="Right-Click_Behavior_in_DML"></span><span id="right-click_behavior_in_dml"></span><span id="RIGHT-CLICK_BEHAVIOR_IN_DML"></span>DML での右クリック動作


右クリック動作は DML で使用できます。 このサンプルでは、altlink を使用して右クリック動作を定義し、 &lt; &gt; ブレークポイントの[**Bp (ブレークポイントの設定)**](bp--bu--bm--set-breakpoint-.md)コマンドを送信し、通常のクリックで[**u (unassemble)**](u--unassemble-.md)を送信する方法を示します。

```text
<link cmd="u MyProgram!memcpy">
<altlink name="Set Breakpoint (bp)" cmd="bp MyProgram!memcpy" />
u MyProgram!memcpy
</link>
```

## <a name="span-iddml_tag_referencespanspan-iddml_tag_referencespanspan-iddml_tag_referencespandml-tag-reference"></a><span id="DML_Tag_Reference"></span><span id="dml_tag_reference"></span><span id="DML_TAG_REFERENCE"></span>DML タグリファレンス


### <a name="span-id_link_spanspan-id_link_spanltlinkgt"></a><span id="_link_"></span><span id="_LINK_"></span>&lt;リンク&gt;

*&lt;link \[ name = "text" \] \[ cmd = "debugger \_ command" \] \[ alt = "表示するテキストをポイントする" \] \[ セクション = "名前" \] &gt; リンクテキスト &lt; /link&gt;*

Link タグは、DML の基本的なハイパーリンクメカニズムです。 DML プレゼンテーションをサポートするユーザーインターフェイスに、リンクテキストをクリック可能なリンクとして表示するように指示します。 Cmd を指定したリンクがクリックされると、デバッガーコマンドが実行され、その出力が現在の出力と置き換えられます。

Name および section 引数を使用すると、HTML の名前と名前のサポートに似た名前付きリンク間のナビゲーションが可能に &lt; &gt; \# なります。 セクションの引数を持つリンクがクリックされると、UI では、名前が一致するリンクがスキャンされ、そのリンクがビューにスクロールされます。 これにより、リンクを同じページ (または新しいページの特定のセクション) の異なるセクションにポイントすることができます。 DML のセクション名は、新しい構文を定義しなくても、コマンド文字列の末尾にセクション名を指定できるようにするために使用します。

プレーンテキストへの変換では、タグが削除されます。

**例**

```text
<b> Handy Links </b>
<link cmd="!dml_proc">Display process information with DML rendering.</link>
<link cmd="kM">Display stack information with DML rendering.</link>
```

**例**

この例では、alt 属性を使用して、DML リンクをポイントしたときに表示されるテキストを作成する方法を示します。

```text
<b>Hover Example</b>
<link cmd="lmD" alt="This link will run the list modules command and display the output in DML format">LmD</link>
```

### <a name="span-id_altlink_spanspan-id_altlink_spanltaltlinkgt"></a><span id="_altlink_"></span><span id="_ALTLINK_"></span>&lt;altlink&gt;

*&lt;altlink \[ name = "text" \] \[ cmd = "debugger \_ command" \] \[ section = "name" \] &gt; alt link text &lt; /altlink&gt;*

&lt;Altlink タグは、 &gt; DML で使用できる右クリックの動作を提供します。 Cmd を指定したリンクがクリックされると、デバッガーコマンドが実行され、その出力が現在の出力と置き換えられます。 &lt; &gt; 通常の &lt; &gt; 右クリック動作をサポートするために、[altlink] タブは通常、リンクタグとペアになっています。

プレーンテキストへの変換では、タグが削除されます。

**例**

この例では、altlink を使用して右クリック動作を定義し、 &lt; &gt; ブレークポイントの[**Bp (ブレークポイントの設定)**](bp--bu--bm--set-breakpoint-.md)コマンドを送信し、通常のクリックで[**u (unassemble)**](u--unassemble-.md)を送信する方法を示します。

```text
<link cmd="u MyProgram!memcpy">
<altlink name="Set Breakpoint (bp)" cmd="bp MyProgram!memcpy" />
u MyProgram!memcpy
</link>
```

### <a name="span-id_exec_spanspan-id_exec_spanltexecgt"></a><span id="_exec_"></span><span id="_EXEC_"></span>&lt;実行&gt;

*&lt;exec cmd = "デバッガー \_ コマンド" &gt; 説明テキスト &lt; /exec&gt;*

Exec タグは link タグに似ています。これは、説明文がクリック可能な項目として表示されることを意味します。 ただし、exec タグがコマンドブラウザーウィンドウで使用されている場合、指定されたコマンドは現在の出力を置き換えずに実行されます。このタグを使用すると、メニューからクリックでコマンドを実行できます。

プレーンテキストへの変換では、タグが削除されます。

**例**

この例では、2つのコマンドを通常のクリックで定義する方法を示します。

```text
<b>Exec Sample</b>
<exec cmd="!dml_proc">Display process information with DML rendering.</exec>
<exec cmd="kM">Display stack information with DML rendering.</exec>
```

### <a name="span-id_b_spanspan-id_b_spanltbgt"></a><span id="_b_"></span><span id="_B_"></span>&lt;b&gt;

*&lt;b &gt; 太字テキスト &lt; /b&gt;*

このタグは太字で要求します。 &lt;B &gt; 、i、および u は、プロパティを &lt; &gt; &lt; &gt; 組み合わせて入れ子にすることができます。

プレーンテキストへの変換では、タグが削除されます。

**例**

この例では、テキストを太字にする方法を示します。

```text
<b>This is bold Text</b>
```

### <a name="span-id_i_spanspan-id_i_spanltigt"></a><span id="_i_"></span><span id="_I_"></span>&lt;私&gt;

*&lt;テキストを斜体にする &gt; &lt; /i&gt;*

このタグは、斜体を要求します。 &lt;B &gt; 、i、および u は、プロパティを &lt; &gt; &lt; &gt; 組み合わせて入れ子にすることができます。

プレーンテキストへの変換では、タグが削除されます。

**例**

この例では、テキストを斜体にする方法を示します。

```text
<i>This is italicized Text</i>
```

### <a name="span-id_u_spanspan-id_u_spanltugt"></a><span id="_u_"></span><span id="_U_"></span>&lt;u&gt;

*&lt;u &gt; 下線付きテキスト &lt; /u&gt;*

このタグは、下線付きのテキストを要求します。 &lt;B &gt; 、i、および u は、プロパティを &lt; &gt; &lt; &gt; 組み合わせて入れ子にすることができます。

プレーンテキストへの変換では、タグが削除されます。

**例**

この例では、テキストに下線を付けています。

```text
<u>This is underlined Text</u>
```

**例**

この例では、タグを太字、下線、斜体に組み合わせる方法を示します。

```text
<b><u><i>This is bold, underlined and italizized text. </i></u></b> 
```

### <a name="span-id_col_spanspan-id_col_spanltcolgt"></a><span id="_col_"></span><span id="_COL_"></span>&lt;行列&gt;

&lt;col fg = "name" bg = "name" &gt; text &lt; /col&gt;

テキストの前景色と背景色を要求します。 色は、表示される色の種類をユーザーが制御できるように、絶対値ではなく既知の色の名前として指定されます。 現在の色の名前 (既定では、WinDbg にのみ適用されます)。

**前景と背景の要素タグ**

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
<td align="left"><p>wbg-Windows の背景</p>
<p>wfg-Windows フォアグラウンド</p></td>
<td align="left">既定のウィンドウの背景色と前景色。 ウィンドウおよびウィンドウテキストのシステムカラーの既定値。
<p>&lt;col fg = "wfg" bg = "wbg" &gt; これは標準の前景/背景のテキスト/ &lt; 列&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>clbg-現在の行の前景</p>
<p>clfg-現在の行の背景</p></td>
<td align="left">現在の線の背景色と前景色。 強調表示および強調表示テキストのシステムカラーを既定値に設定します。
<p>&lt;col fg = "clfg" bg = "clfg" &gt; テストテキスト-現在の行 &lt; /列&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>empbg-強調した背景</p>
<p>emphfg-強調前面</p></td>
<td align="left">強調表示したテキスト。 既定値は薄い青です。
<p>&lt;col fg = "empfg" bg = "empfg" &gt; これは強調表示前/背景テキスト/ &lt; 列&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>subbg-バックグラウンド</p>
<p>subfg-サブフォアグラウンド</p></td>
<td align="left">テキストを入力します。 既定では、非アクティブなキャプションテキストとアクティブでないキャプションのシステムカラーです。
<p>&lt;col fg = "subfg" bg = "subfg" &gt; これは subdued の前景/背景のテキスト/ &lt; 列&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>normbg-標準の背景</p>
<p>normfg-標準の前景</p></td>
<td align="left">標準
<p>&lt;col fg = "normfg" bg = "normbg" &gt; Test Text-Normal (normfg/normbg) &lt; /col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"組み込み"-警告の背景</p>
<p>warnfg-警告の前景</p></td>
<td align="left">警告
<p>&lt;col fg = "warnfg" bg = "" &gt; warnfg "テストテキスト-Warning (/"/")/ &lt; col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>errbg-エラーの背景</p>
<p>errfg-エラーの前景</p></td>
<td align="left">エラー
<p>&lt;col fg = "errfg" bg = "errfg" &gt; テストテキスト-エラー (errfg/errfg)/ &lt; 列&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>verbbg-詳細な背景</p>
<p>verbfg-詳細なフォアグラウンド</p></td>
<td align="left">"詳細"
<p>&lt;col fg = "verbfg" bg = "verbbg" &gt; テストテキスト-Verbose (verbfg/verbbg) &lt; /col&gt;</p></td>
</tr>
</tbody>
</table>



**ソースコードの単一要素タグ**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>srcnum-Source numeric 定数</p></td>
<td align="left">ソース要素の色。
<p>&lt;col fg = "srcnum" bg = "wbg" &gt; テストテキスト-srcnum &lt; /col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcchar-ソース文字定数</p></td>
<td align="left"><p>&lt;col fg = "srcchar" bg = "wbg" &gt; Test Text-srcchar &lt; /col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srcstr-ソース文字列定数</p></td>
<td align="left"><p>&lt;col fg = "srcstr" bg = "wbg" &gt; テストテキスト-srcstr &lt; /col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcid-ソース識別子</p></td>
<td align="left"><p>&lt;col fg = "srcid" bg = "wbg" &gt; テストテキスト-srcid &lt; /col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srckw-キーワード</p></td>
<td align="left"><p>&lt;col fg = "srckw" bg = "wbg" &gt; Test Text-srckw &lt; /col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcpair-Source 中かっこまたは一致するシンボルペア</p></td>
<td align="left"><p>&lt;col fg = "srcpair" bg = "empbbg" &gt; テストテキスト-srcpair &lt; /col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srccmnt-ソースコメント</p></td>
<td align="left"><p>&lt;col fg = "srccmnt" bg = "wbg" &gt; テストテキスト-srccmnt &lt; /col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcdrct-Source ディレクティブ</p></td>
<td align="left"><p>&lt;col fg = "srcdrct" bg = "wbg" &gt; テストテキスト-srcdrct &lt; /col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srcspid-ソースの特殊な識別子</p></td>
<td align="left"><p>&lt;col fg = "srcspid" bg = "wbg" &gt; テストテキスト-srcspid &lt; /col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcannot Source 注釈</p></td>
<td align="left"><p>&lt;col fg = "srcannot ません" bg = "wbg" &gt; テストテキスト-srcannot &lt; /col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>変更された変更データ</p></td>
<td align="left">以前の停止時点以降に変更されたデータ (WinDbg でのレジスタの変更など) に使用されます。 既定値は赤です。
<p>&lt;col fg = "changed" bg = "wbg" &gt; Test Text-changed &lt; /col&gt;</p></td>
</tr>
</tbody>
</table>



## <a name="span-iddml_example_codespanspan-iddml_example_codespanspan-iddml_example_codespandml-example-code"></a><span id="DML_Example_Code"></span><span id="dml_example_code"></span><span id="DML_EXAMPLE_CODE"></span>DML のコード例


このコード例は、次のことを示しています。

-   デバッグコマンドの呼び出し
-   右クリックコマンドの実装
-   実装 (テキストの上にホバーを)
-   色とリッチテキストの使用

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

このコード例は、色と書式設定タグの使用方法を示しています。

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

## <a name="span-iddml_additions_to_the_dbgeng_interfacespanspan-iddml_additions_to_the_dbgeng_interfacespanspan-iddml_additions_to_the_dbgeng_interfacespandml-additions-to-the-dbgeng-interface"></a><span id="DML_Additions_to_the_dbgeng_Interface"></span><span id="dml_additions_to_the_dbgeng_interface"></span><span id="DML_ADDITIONS_TO_THE_DBGENG_INTERFACE"></span>Dbgeng インターフェイスへの DML の追加


[デバッガーエンジンと拡張 api](debugger-engine-and-extension-apis.md)には、デバッガーエンジンを使用してカスタムアプリケーションを作成するためのインターフェイスが用意されています。 WinDbg、KD、CDB、NTSD で実行されるカスタム拡張機能を作成することもできます。 詳細については、「 [DbgEng 拡張機能の記述](writing-dbgeng-extensions.md)」を参照してください。 このセクションでは、デバッガーエンジンインターフェイスに使用できる DML の機能強化について説明します。

Dbgeng には、既にテキスト処理の入力メソッドと出力インターフェイスのセットがあります。 DML を使用する場合は、入力テキストおよび出力テキストで使用されるコンテンツの種類を指定するだけで済みます。

**Dbgeng に DML コンテンツを提供する**

出力コントロールフラグ DEBUG \_ outctl DML は、 \_ dbgeng メソッドによって生成されたテキストを DML コンテンツとして処理する必要があることを示します。 このフラグが指定されていない場合、テキストはプレーンテキストのコンテキストとして扱われます。 デバッグ \_ outctl \_ DML は、次のメソッドで使用できます。

-   [**IDebugControl4:: Controlの出力**](https://msdn.microsoft.com/library/windows/hardware/ff539248)
-   [**IDebugControl4::ControlledOutputVaList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-controlledoutputvalist)
-   [**IDebugControl4:: Control Outputwide**](https://msdn.microsoft.com/library/windows/hardware/ff539266)
-   [**IDebugControl4::ControlledOutputVaListWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-controlledoutputvalistwide)

指定されたテキストは、有効な文字について DML 規則に従う必要があります。

すべての出力ルーチンが拡張され、新しい書式指定子% \[ h | w \] Y {t} を使用できるようになりました。 この書式指定子は、引数として文字列ポインターを持ち、指定されたテキストがプレーンテキストであり、出力処理中に DML 形式に変換される必要があることを示します。 これにより、呼び出し元は dml 形式自体に事前に変換することなく、DML コンテンツにプレーンテキストを簡単に含めることができます。 H と w の修飾子は、% s と同様に、ANSI または Unicode のテキストを示します。

次の表は、% Y 書式指定子の使用方法をまとめたものです。

**% Y {t}**: 引用符で囲まれた文字列です。 出力形式 (最初の引数) が DML の場合、はテキストを DML に変換します。

**% Y {T}**: 引用符で囲まれた文字列です。 は、出力形式に関係なく、常にテキストを DML に変換します。

**% Y {s}**: 引用符で囲まれていない文字列です。 出力形式 (最初の引数) が DML の場合、はテキストを DML に変換します。

**% Y {S}**: 引用符で囲まれていない文字列です。 は、出力形式に関係なく、常にテキストを DML に変換します。

**% Y {as}**: ULONG64。 デバッガーの書式設定されたポインターフィールドの上位32ビットの部分に埋め込むために、空の文字列または9文字のスペースを追加します。 余分なスペースによって9つのスペースが出力されます。これには、上位8個のゼロと文字が含まれ \` ます。

**% Y {ps}**: ULONG64。 デバッガーの書式設定されたポインターフィールド (上位8個のゼロと文字を含む) を埋め込むための余分な領域 \` 。

**% Y {l}**: ULONG64。 ソース行情報としてのアドレス。




このコードスニペットは、% Y 書式指定子の使用方法を示しています。

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

このサンプルコードでは、次の出力が生成されます。

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

追加の制御フラグ (デバッグ \_ outctl \_ アンビエント \_ DML) を使用すると、出力の制御属性を変更せずに dml コンテキストテキストを指定できます。 デバッグ \_ outctl \_ アンビエント \_ テキストも、以前に存在していたデバッグ outctl アンビエントのわかりやすい別名として追加されてい \_ \_ ます。 出力制御フラグは、dbgeng. h で定義されています。

```cpp
#define DEBUG_OUTCTL_DML               0x00000020

// Special values which mean leave the output settings
// unchanged.
#define DEBUG_OUTCTL_AMBIENT_DML       0xfffffffe
#define DEBUG_OUTCTL_AMBIENT_TEXT      0xffffffff

// Old ambient flag which maps to text.
#define DEBUG_OUTCTL_AMBIENT           DEBUG_OUTCTL_AMBIENT_TEXT
```

**デバッグ対象からの DML コンテンツの提供**

Dbgeng は、特定のマーカーのデバッグ対象の出力をスキャンするように拡張されています。つまり、デバッグ対象の出力の残りのテキストを DML として扱う必要があることを示します。 モードの変更は、1つの OutputDebugString 文字列などの1つのデバッグ対象出力にのみ適用され、グローバルモードスイッチではありません。

この例では、plain と DML の両方の出力が混在しています。

```text
OutputDebugString(“This is plain text\n<?dml?>This is <col fg=\”emphfg\”>DML</col> text\n”);
```

生成された出力には、テキストの行が続き、dml が別の色で表示されます。

**IDebugOutputCallbacks2**

IDebugOutputCallbacks2 を使用すると、dbgeng インターフェイスクライアントはプレゼンテーション用の完全な DML コンテンツを受信できます。 IDebugOutputCallbacks2 は、IDebugOutputCallbacks (not IDebugOutputCallbacksWide) の拡張機能であり、既存の SetOutputCallbacks バックメソッドに渡すことができます。 エンジンは、IDebugOutputCallbacks2 の QueryInterface を使用して、受信出力コールバックオブジェクトがサポートするインターフェイスを確認します。 オブジェクトが IDebugOutputCallbacks2 をサポートしている場合、すべての出力は拡張 IDebugOutputCallbacks2 メソッドを介して送信されます。基本的な IDebugOutputCallbacks:: Output メソッドは使用されません。

新しいメソッドは次のとおりです。

-   IDebugOutputCallbacks2:: GetInterestMask –コールバックオブジェクトが、受信する出力通知の種類を記述できるようにします。 基本的な選択肢は、プレーンテキストコンテンツ (デバッグ \_ outcbi \_ テキスト) と DML コンテンツ (デバッグ \_ outcbi \_ DML) です。 また、コールバックオブジェクトは、明示的なフラッシュの通知を要求することもできます (デバッグ \_ outcbi \_ explicit \_ フラッシュ)。
-   IDebugOutputCallbacks2:: Output2 –すべての IDebugOutputCallbacks2 通知は、Output2 を経由します。 Flags、Arg、および Text パラメーターが通知ペイロードを保持しているときに、どの種類の通知を受信するかを示すパラメーターです。 通知は次のとおりです。

    -   DEBUG \_ outcb \_ Text – Plain text の出力。 フラグはデバッグ \_ outcbf からのもの \_ \* で、Arg は出力マスク、テキストはプレーンテキストです。 これは \_ 、対象マスクで DEBUG outcbi \_ テキストが指定されている場合にのみ受信されます。

    -   デバッグ \_ outcb \_ DML – dml コンテンツ出力。 フラグはデバッグ \_ outcbf からのもの \_ \* で、Arg は出力マスク、テキストは DML コンテンツです。 これは \_ 、対象マスクでデバッグ outcbi \_ DML が指定されている場合にのみ受信されます。
    
    -   デバッグ \_ outcb \_ EXPLICIT \_ フラッシュ–呼び出し元は、バッファーに含まれるテキストなしで flushcallbacks バックを呼び出しました。 通常、バッファー内のテキストをフラッシュすると、DEBUG \_ outcbf \_ 組み合わせの \_ 明示的な \_ フラッシュフラグが設定され、2つの通知が1つにまとめられます。 テキストがバッファリングされていない場合は、フラッシュのみの通知が送信されます。

 次に示すように、関心のマスクフラグは dbgeng .h で定義されています。

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

出力オブジェクトは、両方のコンテンツを処理できる場合に、テキストと DML の両方のコンテンツに登録できることに注意してください。 コールバックの出力処理中に、エンジンは変換を減らす形式を選択するため、両方をサポートするとエンジンでの変換が減少する可能性があります。 ただし、必要ではありませんが、1つの形式のみをサポートすることが期待される操作モードです。

**自動変換**

Dbgeng は、必要に応じて、プレーンテキストと DML を自動的に変換します。 たとえば、呼び出し元が DML コンテンツをエンジンに送信する場合、エンジンは、プレーンテキストのみを受け入れるすべての出力クライアントのプレーンテキストに変換します。 また、DML のみを受け入れるすべての出力コールバックに対して、エンジンはプレーンテキストを DML に変換します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバッガー マークアップ言語の使用](debugger-markup-language-commands.md)










