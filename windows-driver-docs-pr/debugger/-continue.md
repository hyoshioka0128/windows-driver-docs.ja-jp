---
title: .continue
description: .Continue トークンは、c 言語で continue キーワードと同様に動作します。
ms.assetid: c8f6c69c-d912-4ce4-a9c2-d82c349484a9
keywords:
- .continue Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .continue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e087d011f7978d935b7ba9dfb8a7450dff71610e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558760"
---
# <a name="continue"></a>.continue


**.Continue**トークンと同様に動作、**続行**C のキーワード

```dbgsyntax
.for (...) { ... ; .if (Condition) .continue ; ... } 

.while (...) { ... ; .if (Condition) .continue ; ... } 

.do { ... ; .if (Condition) .continue ; ... } (...) 
```

## <span id="ddk_token_continue_dbg"></span><span id="DDK_TOKEN_CONTINUE_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>注釈
-------

**.Continue**内でトークンを使用できます[**対して**](-for.md)、 [ **.while**](-while.md)、または[**手順**](-do.md)ループします。

C goto ステートメントと同じコントロール フロー トークンがないため、通常使用する、 **.continue**内でトークンを[ **.if** ](-if.md)構文に示すように、条件付き上記の例です。 ただし、これは実際に必要ではありません。

 

 





