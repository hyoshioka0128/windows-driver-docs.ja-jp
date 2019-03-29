---
title: (式の評価)
description: 疑問符 () のコマンドは、評価し、式の値を表示します。コマンドのヘルプを表示します () を単独で疑問符 () を確認します。
ms.assetid: fae689b3-47c9-44bd-992d-8344805fb4b7
keywords:
- (式の評価)Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Evaluate Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0a3314967d8b9b9249a8c66ca0889ec536c90308
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572503"
---
# <a name="-evaluate-expression"></a>? (式の評価)


疑問符 () (**?**) コマンドを評価し、式の値を表示します。

**注**  単独の疑問符 ([**?**](---command-help-.md)) コマンドのヘルプを表示します。 **でしょうか。** *式*コマンドは、指定された式を評価します。

```dbgcmd
    ? Expression
```

## <a name="span-idddkcmdevaluateexpressiondbgspanspan-idddkcmdevaluateexpressiondbgspanparameters"></a><span id="ddk_cmd_evaluate_expression_dbg"></span><span id="DDK_CMD_EVALUATE_EXPRESSION_DBG"></span>パラメーター


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
評価する式を指定します。

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

 

<a name="remarks"></a>コメント
-------

入力と出力の**でしょうか。** コマンドは、MASM 式の構文または C++ 式の構文を使用しているかどうかによって異なります。 この種の式の構文の詳細については、次を参照してください。[を評価する式](evaluating-expressions.md)と[数値式の構文](numerical-expression-syntax.md)します。

MASM の構文を使用している場合、入力と出力は現在の基数に依存します。 基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。

**でしょうか。** コマンドは、現在のスレッドとプロセスのコンテキストで式内のシンボルを評価します。

一部の文字列がなど、エスケープを含めること **\\n**、  **\\"**、  **\\r**、および **\\b**、するは文字どおり、読み取り専用ではなく、エバリュエーターによって解釈されます。 エスケープ文字列内のエバリュエーターによって解釈の評価でエラーが発生することができます。 以下に例を示します。

```console
0:000> as AliasName c:\dir\name.txt
0:000> al
  Alias            Value
 -------          -------
 AliasName        c:\dir\name.txt
0:001> ? $spat( "c:\dir\name.txt", "*name*" )
Evaluate expression: 0 = 00000000
0:001> ? $spat( "${AliasName}", "*name*" )
Evaluate expression: 0 = 00000000
0:001> ? $spat( "c:\dir\", "*filename*" )
Syntax error at '( "c:\dir\", "*filename*" )
```

最初の 2 つの例では、文字列がパターンに一致していて、エバリュエーターが値を返すことの**FALSE**します。 第 3 回目、エバリュエーターことはできません比較文字列の末尾に円記号であるため ( \\ )、そのため、  **\\"** エバリュエーターによって変換されます。

リテラル文字列を解釈するエバリュエーターを取得することを使用する必要があります、 <strong>@"</strong>*文字列*<strong>"</strong>構文。 次のコード例では、正しい結果を示します。

```console
0:000> ? $spat( @"c:\dir\name.txt", "*name*" )
Evaluate expression: 1 = 00000000`00000001
0:000> ? $spat( @"${AliasName}", "*name*" )
Evaluate expression: 1 = 00000000`00000001
0:001> ? $spat( @"c:\dir\", "*filename*" )
Evaluate expression: 0 = 00000000
```

上記の例で、 **$spat** MASM 演算子が (大文字) と一致するかどうかを判断する最初の文字列を確認します。 2 番目の文字列のパターン。 MASM の演算子の詳細については、次を参照してください。、 [MASM 数字と演算子](masm-numbers-and-operators.md)トピック。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**??(C++ の式の評価)**](----evaluate-c---expression-.md)

[**.formats (数値の形式を表示する)**](-formats--show-number-formats-.md)

 

 






