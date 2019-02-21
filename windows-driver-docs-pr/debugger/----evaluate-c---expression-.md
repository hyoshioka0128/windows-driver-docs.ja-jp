---
title: (C++ の式の評価)
description: 二重の疑問符 () のコマンドは、評価し、C++ の式の規則に従って、式の値を表示します。
ms.assetid: 3a15a0a3-03d0-4807-a6df-054de819c0a0
keywords:
- (C++ の式の評価)Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Evaluate C++ Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d87d24430baa315e9e0ec45fdbdb21eb441f76ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535462"
---
# <a name="-evaluate-c-expression"></a>?? (C++ の式の評価)


二重の疑問符 (**??**) コマンドを評価し、C++ の式の規則に従って、式の値を表示します。

```dbgcmd
    ?? Expression
```

## <a name="span-idddkcmdevaluatecexpressiondbgspanspan-idddkcmdevaluatecexpressiondbgspanparameters"></a><span id="ddk_cmd_evaluate_c_expression_dbg"></span><span id="DDK_CMD_EVALUATE_C_EXPRESSION_DBG"></span>パラメーター


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
C++ の式を評価するを指定します。 構文の詳細については、次を参照してください。 [C++ 数字と演算子](c---numbers-and-operators.md)します。

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

 

<a name="remarks"></a>注釈
-------

**??** コマンドは、現在のスレッドとプロセスのコンテキストで式内のシンボルを評価します。

一部を評価する場合、**式**MASM 式の規則に従って式がその一部をかっこで囲むし、追加の 2 つのアット ( **@@** ) する前にします。 MASM の式と C++ の式の詳細については、次を参照してください。[を評価する式](evaluating-expressions.md)と[数値式の構文](numerical-expression-syntax.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**?(式の評価)**](---evaluate-expression-.md)

[**.formats (数値の形式を表示する)**](-formats--show-number-formats-.md)

 

 






