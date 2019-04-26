---
title: .for
description: 対してトークンと同様に動作、C でキーワードの複数の増分値を除くコマンドする必要がありますセミコロンで区切って、コンマではありません。
ms.assetid: 35f54c4c-e7f5-42a9-b579-1e4958b7286b
keywords:
- 対して Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .for
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09e3d3fc802c7a81aa9e1564a1bb7ee6f6d52fd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336633"
---
# <a name="for"></a>.for


**対して**トークンと同様に動作、**の**キーワード C では、複数の増分値はそのコマンドをコンマではなく、セミコロンで区切る必要があります。

```dbgcmd
.for (InitialCommand ; Condition ; IncrementCommands) { Commands } 
```

## <a name="span-idddktokenfordbgspanspan-idddktokenfordbgspansyntax-elements"></a><span id="ddk_token_for_dbg"></span><span id="DDK_TOKEN_FOR_DBG"></span>構文要素


<span id="_______InitialCommand______"></span><span id="_______initialcommand______"></span><span id="_______INITIALCOMMAND______"></span> *InitialCommand*   
ループを開始する前に実行されるコマンドを指定します。 最初のコマンドは 1 つのみが許可されます。

<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *条件*   
条件を指定します。 これは、0 に評価されると、false; として扱われますそれ以外の場合は true です。 それを囲む*条件*かっこは省略可能です。 *条件*デバッガー コマンドではなく、式を指定する必要があります。 (MASM または C++) の既定式エバリュエーターによって評価されます。 詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

<span id="_______IncrementCommands______"></span><span id="_______incrementcommands______"></span><span id="_______INCREMENTCOMMANDS______"></span> *IncrementCommands*   
各ループの終了時に実行される 1 つまたは複数のコマンドを指定します。 複数の増分コマンドを使用する場合は、セミコロンで区切りますが、中かっこで囲むを表示できません。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *コマンド*   
条件が true、繰り返し実行される 1 つまたは複数のコマンドを指定します。 コマンドのブロックは、1 つのコマンドで構成されている場合でも、中かっこで囲む必要があります。 複数のコマンドは、前に、右中かっこは、セミコロンの後に指定する必要はありませんが、セミコロンで、最後のコマンドで区切る必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>注釈
-------

すべての作業は、増分コマンドによって実行されていたが場合、は、省略*条件*完全かつ簡単には、中かっこの空のペアを使用します。

次の例に示します、**対して**ステートメントを複数のインクリメント コマンド。

```dbgcmd
0:000> .for (r eax=0; @eax < 7; r eax=@eax+1; r ebx=@ebx+1) { .... }
```

[ **.Break** ](https://msdn.microsoft.com/library/windows/hardware/ff556242)と[ **.continue** ](-continue.md)を終了または再起動のトークンを使用できます、*コマンド*ブロックします。

 

 





