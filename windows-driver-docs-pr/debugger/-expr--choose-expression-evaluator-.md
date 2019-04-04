---
title: .expr (式エバリュエーターの選択)
description: .Expr コマンドでは、既定の式エバリュエーターを指定します。
ms.assetid: 96d246c2-10fe-4688-a04f-1325ac51e4b3
keywords:
- .expr (式エバリュエーターを選択します) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .expr (Choose Expression Evaluator)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 54e745cb7c255e0503ce62f83f90c5b01e2c8693
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578313"
---
# <a name="expr-choose-expression-evaluator"></a>.expr (式エバリュエーターの選択)


**.Expr**コマンドが既定の式エバリュエーターを指定します。

```dbgcmd
.expr /s masm 
.expr /s c++ 
.expr /q 
.expr 
```

## <a name="span-idddkmetachooseexpressionevaluatordbgspanspan-idddkmetachooseexpressionevaluatordbgspanparameters"></a><span id="ddk_meta_choose_expression_evaluator_dbg"></span><span id="DDK_META_CHOOSE_EXPRESSION_EVALUATOR_DBG"></span>パラメーター


<span id="________s_masm______"></span><span id="________S_MASM______"></span> **/s masm**   
式エバリュエーターの Microsoft アセンブラー (MASM) の既定の式の種類を変更します。 この型は、デバッガーを起動するときに、既定値です。

<span id="________s_c________"></span><span id="________S_C________"></span> **/s c++**   
C++ の式エバリュエーターを既定の式の種類を変更します。

<span id="________q______"></span><span id="________Q______"></span> **/q**   
可能な式の型の一覧が表示されます。

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

使用すると、 **.expr**デバッガーを表示する現在の既定の式の型、引数を指定しないでコマンドします。

[**いますか。(C++ の式の評価)** ](----evaluate-c---expression-.md)のコマンドは、[ウォッチ] ウィンドウで、および[[ローカル] ウィンドウ](locals-window.md)常に C++ 式の構文を使用します。 その他のすべてのコマンドとデバッグ情報のウィンドウは、既定の式エバリュエーターを使用します。

どの構文を使用するかを制御する方法の詳細については、[を評価する式](evaluating-expressions.md)を参照してください。 構文の詳細については、[数値式の構文](numerical-expression-syntax.md)を参照してください。

 

 





