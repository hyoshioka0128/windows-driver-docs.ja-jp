---
title: '\# (逆アセンブリのパターンの検索)'
description: 番号記号 (#) のコマンドは、逆アセンブリ コードで指定したパターンを検索します。
ms.assetid: 834dd432-94b8-4bf6-9318-09a118eab5ab
keywords:
- (逆アセンブリのパターンの検索)Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Search for Disassembly Pattern)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25968c3ee037e332a0d532a6da9988b96261cc57
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337059"
---
# <a name="-search-for-disassembly-pattern"></a>\# (逆アセンブリのパターンの検索)


シャープ記号 ( **\#** ) コマンドの逆アセンブリ コード内の指定したパターンを検索します。

```dbgcmd
     # [Pattern] [Address [ L Size ]] 
```

## <a name="span-idddkcmdsearchfordisassemblypatterndbgspanspan-idddkcmdsearchfordisassemblypatterndbgspanparameters"></a><span id="ddk_cmd_search_for_disassembly_pattern_dbg"></span><span id="DDK_CMD_SEARCH_FOR_DISASSEMBLY_PATTERN_DBG"></span>パラメーター


<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *パターン*   
逆アセンブリ コード内で検索するパターンを指定します。 *パターン*さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。 内のスペースを含める場合*パターン*パターンを引用符で囲む必要があります。 パターンは、大文字小文字が区別されません。 使用していた場合、 **\#** コマンドと省略*パターン*コマンドの再利用が最も最近使用したパターン。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
検索を開始アドレスを指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *サイズ*   
検索する命令の数を指定します。 省略した場合*サイズ*検索は、最初の一致が発生するまで継続します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

アセンブリの詳細については、デバッグ、および関連するコマンドを参照してください[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

<a name="remarks"></a>コメント
-------

使用していた場合、 **\#** コマンドと省略*アドレス*、前回の検索が終了した位置から検索が開始します。

このコマンドは、指定したパターンの逆アセンブルしたテキストを検索することにより動作します。 このコマンドを使用すると、逆アセンブリの出力にレジスタ名、定数、または表示されるその他の任意の文字列を検索します。 なしのコマンドを繰り返すことができます、*アドレス*パラメーターのパターンの連続する出現位置を検索します。

逆アセンブリ命令を表示するにを使用して、 [**u (Unassemble)** ](u--unassemble-.md) コマンドまたはを使用して、 [逆アセンブル ウィンドウ](disassembly-window.md) WinDbg でします。 逆アセンブリの表示には、最大 4 つの部分が含まれています。アドレスのオフセット、バイナリ コード、アセンブリ言語ニーモニック、およびアセンブリ言語の詳細情報。 次の例では、可能な表示を示します。

```console
0040116b    45          inc         ebp            
0040116c    fc          cld                        
0040116d    8945b0      mov         eax,[ebp-0x1c] 
```

**\#** コマンド内の 1 つの逆アセンブルの表示の部分のテキストを検索できます。 たとえば、使用する **\# eax 0040116b**を検索する、 **mov eax、\[ebp 0x1c\]**  0040116 d のアドレスの命令。 次のコマンドでは、この命令も検索されます。

```console
#  [ebp?0x  0040116b 
#  mov  0040116b 
#  8945*  0040116b 
#  116d  0040116b 
```

検索することはできませんただし、 **mov eax\\** * 1 つの単位としてため**mov**と**eax**表示のさまざまな部分に表示されます。 代わりに、 **mov\*eax**します。

その他の例として、最初の参照を検索する次のコマンドを発行する可能性があります、 **strlen**関数のエントリ ポイント後**メイン**します。

```console
# strlen main
```

同様に、最初に次の 2 つのコマンドを発行することが**jnz**後の命令アドレス 0x779F9FBA とし、次を検索**jnz**その後の命令。

```console
# jnz 779f9fba# 
```

省略した場合*パターン*または*アドレス*、その値がの前の使用に基づいて、 **\#** コマンド。 初めて発行するいずれかのパラメーターを省略したかどうか、 **\#** コマンド、検索は実行されません。 ただし、値の*パターン*と*アドレス*このような状況であっても初期化されます。

含める場合*パターン*または*アドレス*、その値が入力した値に設定します。 省略した場合*アドレス*、プログラム カウンターの現在の値に初期化されます。 省略した場合*パターン*、空のパターンに初期化されます。

 

 





