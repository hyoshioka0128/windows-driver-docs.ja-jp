---
title: .break
description: .Break トークンは、c 言語で break キーワードと同様に動作します。
ms.assetid: 577e74d1-824f-424a-b30e-a82fe2d682f1
keywords:
- .break Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .break
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc0db0a953def999e02f40bfb1674503ecc33a1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556723"
---
# <a name="break"></a>.break


**.Break**トークンと同様に動作、 **break** C のキーワード

```dbgcmd
 .for (...) { ... ; .if (Condition) .break ; ...} 

.while (...) { ... ; .if (Condition) .break ; ...} 

.do { ... ; .if (Condition) .break ; ...} (...) 
```

## <span id="ddk_token_break_dbg"></span><span id="DDK_TOKEN_BREAK_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>注釈
-------

**.Break**内でトークンを使用できます[**対して**](-for.md)、 [ **.while**](-while.md)、または[ **手順**](-do.md)ループします。

C と同じコントロール フロー トークンがないため**goto**ステートメントでは、通常使用する、 **.break**内でトークンを[ **.if** ](-if.md)条件では、上記の構文の例で示すようにします。 ただし、これは実際に必要ではありません。

 

 





