---
title: .elsif
description: .Elsif トークンは、他の場合と同様に動作 C のキーワードの組み合わせ
ms.assetid: f5612326-9fcf-4f2e-9692-cc75e7ff4664
keywords:
- デバッグ .elsif Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .elsif
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e4c5ab3f18f7867f0b47c63e3251aa62028ae6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581738"
---
# <a name="elsif"></a>.elsif


**.Elsif**トークンと同様に動作、 **else if** C のキーワードの組み合わせ

```dbgcmd
.if (Condition) { Commands } .elsif (Condition) { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddktokenelsifdbgspanspan-idddktokenelsifdbgspansyntax-elements"></a><span id="ddk_token_elsif_dbg"></span><span id="DDK_TOKEN_ELSIF_DBG"></span>構文要素


<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *条件*   
条件を指定します。 これは、0 に評価されると、false; として扱われますそれ以外の場合は true です。 それを囲む*条件*かっこは省略可能です。 *条件*デバッガー コマンドではなく、式を指定する必要があります。 (MASM または C++) の既定式エバリュエーターによって評価されます。 詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *コマンド*   
条件付きで実行される 1 つまたは複数のコマンドを指定します。 コマンドのブロックは、1 つのコマンドで構成されている場合でも、中かっこで囲む必要があります。 複数のコマンドは、前に、右中かっこは、セミコロンの後に指定する必要はありませんが、セミコロンで、最後のコマンドで区切る必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

 

 





