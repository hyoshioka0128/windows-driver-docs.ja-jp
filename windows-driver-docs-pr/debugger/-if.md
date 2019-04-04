---
title: .if でレジスタ
description: .If トークンが、場合のように動作 C のキーワード
ms.assetid: ccd74461-759f-400d-90da-efba2e4498e6
keywords:
- .if でレジスタの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .if
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1dfb6195be3945914fd5d119c53c2607baac7e6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539281"
---
# <a name="if"></a>.if でレジスタ


**.If**トークンと同様に動作、**場合**C のキーワード

```dbgcmd
.if (Condition) { Commands } 

.if (Condition) { Commands } .else { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddktokenifdbgspanspan-idddktokenifdbgspansyntax-elements"></a><span id="ddk_token_if_dbg"></span><span id="DDK_TOKEN_IF_DBG"></span>構文要素


<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *条件*   
条件を指定します。 これは、0 に評価されると、false; として扱われますそれ以外の場合は true です。 それを囲む*条件*かっこは省略可能です。 *条件*デバッガー コマンドではなく、式を指定する必要があります。 (MASM または C++) の既定式エバリュエーターによって評価されます。 詳細については、[数値式の構文](numerical-expression-syntax.md)を参照してください。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *コマンド*   
条件付きで実行される 1 つまたは複数のコマンドを指定します。 コマンドのブロックは、1 つのコマンドで構成されている場合でも、中かっこで囲む必要があります。 複数のコマンドは、前に、右中かっこは、セミコロンの後に指定する必要はありませんが、セミコロンで、最後のコマンドで区切る必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)を参照してください。

 

 





