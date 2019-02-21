---
title: .else
description: .Else トークンが C の else キーワードと同様に動作します。
ms.assetid: aa783a66-2b28-40d1-a943-67a26e668612
keywords:
- .else Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .else
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5d82180b5efcbdf4b89252e17a71979be55099f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549937"
---
# <a name="else"></a>.else


**.Else**トークンと同様に動作、**他**C のキーワード

```dbgcmd
.if (Condition) { Commands } .else { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddktokenelsedbgspanspan-idddktokenelsedbgspansyntax-elements"></a><span id="ddk_token_else_dbg"></span><span id="DDK_TOKEN_ELSE_DBG"></span>構文要素


<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *コマンド*   
条件付きで実行される 1 つまたは複数のコマンドを指定します。 コマンドのブロックは、1 つのコマンドで構成されている場合でも、中かっこで囲む必要があります。 複数のコマンドは、前に、右中かっこは、セミコロンの後に指定する必要はありませんが、セミコロンで、最後のコマンドで区切る必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

 

 





