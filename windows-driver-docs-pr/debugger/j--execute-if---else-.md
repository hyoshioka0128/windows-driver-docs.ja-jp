---
title: j (場合の実行 - その他)
description: J コマンドを使用して、指定された式の評価によって、指定されたコマンドのいずれかの条件付きで実行します。
ms.assetid: c6bb2415-e888-458b-8fb9-9d50b90cc531
keywords:
- j (場合の実行 - その他) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- j (Execute If - Else)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8030afbb9018c7063104c288c10ac46be94b6cc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530979"
---
# <a name="j-execute-if---else"></a>j (場合の実行 - その他)


**J**コマンドが条件付きで指定された式の評価によって、指定されたコマンドの 1 つを実行します。

```dbgcmd
j Expression Command1 ; Command2 
j Expression 'Command1' ; 'Command2' 
```

## <a name="span-idddkcmdexecuteifelsedbgspanspan-idddkcmdexecuteifelsedbgspanparameters"></a><span id="ddk_cmd_execute_if_else_dbg"></span><span id="DDK_CMD_EXECUTE_IF_ELSE_DBG"></span>パラメーター


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
評価する式。 この式が 0 以外の値に評価される場合*Command1*を実行します。 この式が 0 に評価される場合*Command2*を実行します。 この式の構文の詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

<span id="_______Command1______"></span><span id="_______command1______"></span><span id="_______COMMAND1______"></span> *Command1*   
場合に実行されるコマンド文字列内の式*式*0 以外の値 (TRUE) に評価されます。 コマンド文字列に単一引用符で囲むと、複数のコマンドを組み合わせることができます ( **'** ) し、セミコロンで区切ってコマンドを分離します。 コマンド文字列が 1 つのコマンドである場合は、単一引用符は省略可能です。

<span id="_______Command2______"></span><span id="_______command2______"></span><span id="_______COMMAND2______"></span> *Command2*   
場合に実行されるコマンド文字列内の式*式*0 (FALSE) に評価されます。 コマンド文字列に単一引用符で囲むと、複数のコマンドを組み合わせることができます ( **'** ) し、セミコロンで区切ってコマンドを分離します。 コマンド文字列が 1 つのコマンドである場合は、単一引用符は省略可能です。

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

セミコロンまたはその他のコマンドの後に追加することはできません、 **j**コマンド。 後にセミコロンが表示された場合*Command2*、すべての後、セミコロンは無視されます。

次のコマンドの値を表示する**eax**場合**MySymbol**ゼロに等しくの値を表示します**ebx**と**ecx**それ以外の場合。

```dbgcmd
0:000> j (MySymbol=0) 'r eax'; 'r ebx; r ecx' 
```

単一引用符を省略することもできます**r eax**がこれらのコマンドは、読みやすきます。 コマンドのいずれかを省略する場合は、空の引用符を含めるまたは、次のコマンドのように、そのコマンドのパラメーターを省略できます。

```dbgcmd
0:000> j (MySymbol=0) ''; 'r ebx; r ecx' 
0:000> j (MySymbol=0)  ; 'r ebx; r ecx' 
```

使用することも、 **j**他のコマンド内でコマンド。 たとえば、使用することができます、 **j**条件付きブレークポイントを作成するコマンド。

```dbgcmd
0:000> bp `mysource.cpp:143` "j (poi(MyVar)>0n20) ''; 'gc' "
```

条件付きブレークポイントの構文の詳細については、次を参照してください。 [、条件付きブレークポイント](setting-a-conditional-breakpoint.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**z (実行中に)**](z--execute-while-.md)

 

 






