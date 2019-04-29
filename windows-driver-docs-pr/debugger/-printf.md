---
title: .printf
description: C 言語で printf ステートメントのように動作する .printf トークン
ms.assetid: 16ad25c4-7df3-490e-80da-2beaddec3230
keywords:
- デバッグ .printf Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .printf
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 04ab8f9d5a680c1b5118a2b051e64ed7d156a6ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334388"
---
# <a name="printf"></a>.printf


**.Printf**トークンと同様に動作、 **printf** c 言語でステートメント

```dbgcmd
.printf [/D] [Option] "FormatString" [, Argument , ...] 
```

## <a name="span-idsyntaxelementsspanspan-idsyntaxelementsspanspan-idsyntaxelementsspansyntax-elements"></a><span id="Syntax_Elements"></span><span id="syntax_elements"></span><span id="SYNTAX_ELEMENTS"></span>構文要素


<span id="_D"></span><span id="_d"></span>**/D**  
書式指定文字列が含まれているを指定します。[デバッガー Markup Language](debugger-markup-language-commands.md) (DML)。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *オプション*   
(WinDbg のみ)WinDbg として書式文字列を解釈する必要がありますテキスト メッセージの種類を指定します。 WinDbg は、それぞれのデバッガー コマンド ウィンドウ メッセージをバック グラウンドの種類とテキストの色を割り当てますこれらのオプションのいずれかを選択すると、適切な色で表示するメッセージ。 既定では、標準レベルのメッセージとしてテキストを表示します。 メッセージの色とその設定方法の詳細については、次を参照してください[ビュー |。オプション](view---options.md)します。

次のオプションを使用できます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">メッセージの種類</th>
<th align="left">[オプション] ダイアログ ボックスの色のタイトル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>/od</p></td>
<td align="left"><p>デバッグ対象</p></td>
<td align="left"><p>デバッグ対象レベルのコマンド ウィンドウ</p></td>
</tr>
<tr class="even">
<td align="left"><p>/oD</p></td>
<td align="left"><p>デバッグ対象のプロンプト</p></td>
<td align="left"><p>デバッグ対象のレベルをコマンド プロンプト ウィンドウ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/oe</p></td>
<td align="left"><p>error (エラー)</p></td>
<td align="left"><p>エラー レベルのコマンド ウィンドウ</p></td>
</tr>
<tr class="even">
<td align="left"><p>/on</p></td>
<td align="left"><p>標準</p></td>
<td align="left"><p>通常のレベルのコマンド ウィンドウ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/op</p></td>
<td align="left"><p>prompt</p></td>
<td align="left"><p>レベルをコマンド プロンプト ウィンドウ</p></td>
</tr>
<tr class="even">
<td align="left"><p>/oP</p></td>
<td align="left"><p>プロンプトを登録します。</p></td>
<td align="left"><p>プロンプト レベルのコマンド ウィンドウを登録します</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/os</p></td>
<td align="left"><p>シンボル</p></td>
<td align="left"><p>シンボルのメッセージ レベルのコマンド ウィンドウ</p></td>
</tr>
<tr class="even">
<td align="left"><p>/ov</p></td>
<td align="left"><p>詳細</p></td>
<td align="left"><p>詳細なレベルのコマンド ウィンドウ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/ow</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>警告レベルのコマンド ウィンドウ</p></td>
</tr>
</tbody>
</table>

 

<span id="_______FormatString______"></span><span id="_______formatstring______"></span><span id="_______FORMATSTRING______"></span> *FormatString*   
書式指定文字列を指定します。 **printf**します。 一般に、変換の文字が C. 同様に機能します。浮動小数点の変換の文字の 64 ビットの引数が 32 ビットの浮動小数点数として解釈しない限り、 **l**修飾子を使用します。

"I64"修飾子は、値を 64 ビットとして解釈することを示すために追加できます。 たとえば、64 ビットの 16 進数を印刷する「が %i64x」を使用できます。

%P の変換の文字がサポートされていますが、ターゲットの仮想アドレス空間内のポインターを表します。 修飾子がないと、書式設定、デバッガーの内部アドレスを使用しています。 だけでなく、標準の printf 書式指定子、次の追加の変換の文字はサポートされています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">文字</th>
<th align="left">引数の型</th>
<th align="left">引数</th>
<th align="left">テキスト出力</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%p</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>ターゲットの仮想アドレス空間内のポインターです。</p></td>
<td align="left"><p>ポインターの値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%N</p></td>
<td align="left"><p>DWORD_PTR (32 ビットまたは 64 ビット、ホストのアーキテクチャに応じて)</p></td>
<td align="left"><p>ホストの仮想アドレス空間内のポインターです。</p></td>
<td align="left"><p>ポインターの値。 (これは標準の C %p 文字に相当) です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>% の ma</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>ターゲットの仮想アドレス空間内の NULL で終わる ASCII 文字列のアドレス。</p></td>
<td align="left"><p>指定された文字列。</p></td>
</tr>
<tr class="even">
<td align="left"><p>% mu</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>ターゲットの仮想アドレス空間内の NULL で終わる Unicode 文字列のアドレス。</p></td>
<td align="left"><p>指定された文字列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>% msa</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>ターゲットの仮想アドレス空間で ANSI_STRING 構造体のアドレス。</p></td>
<td align="left"><p>指定された文字列。</p></td>
</tr>
<tr class="even">
<td align="left"><p>% msu</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>ターゲットの仮想アドレス空間内の UNICODE_STRING 構造体のアドレス。</p></td>
<td align="left"><p>指定された文字列。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%y</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>ターゲットの仮想アドレス空間内のデバッガー シンボルのアドレス。</p></td>
<td align="left"><p>指定されたシンボル (と置き換え、存在する場合) の名前を含む文字列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>% ly</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>ターゲットの仮想アドレス空間内のデバッガー シンボルのアドレス。</p></td>
<td align="left"><p>使用可能なソース行情報の指定したシンボル (と置き換え、存在する場合)、名前を含む文字列。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Arguments______"></span><span id="_______arguments______"></span><span id="_______ARGUMENTS______"></span> *引数*   
書式指定文字列の引数を指定します。 **printf**します。 指定された引数の数が変換の文字の数に一致する必要があります*FormatString*します。 各引数は、(MASM または C++) の既定式エバリュエーターによって評価される式です。 詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>コメント
-------

使用して選択できる色の設定、*オプション*パラメーターは既定ですべてに設定白地に黒のテキスト。 これらのオプションを最大限に活用するために、必要があります最初に使用する[ビュー |オプション](view---options.md)オプション ダイアログ ボックスを開き、デバッガー コマンド ウィンドウのメッセージの色の設定を変更します。

次の例では、書式指定文字列で DML タグを含める方法を示します。

```dbgcmd
.printf /D "Click <link cmd=\".chain /D\">here</link> to see extensions DLLs."
```

![コマンドのブラウザー ウィンドウで dml リンクのスクリーン ショット](images/printf01.png)

上の図に示すように出力がで指定されたコマンドを実行することができます をクリックしたリンク、`<link>`タグ。 次の図は、リンクをクリックしての結果を示します。

![コマンドのブラウザー ウィンドウで dml 出力のスクリーン ショット](images/printf02.png)

DML タグについては、Windows のツールのデバッグの dml.doc のインストール フォルダーを参照してください。

 

 





