---
title: .while
description: While のように動作する .while トークン C のキーワード
ms.assetid: bc38357d-b17a-4a26-840e-1b4b90986154
keywords:
- .while Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .while
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c69d2a88516f0048ab2cf87e1d9967e4bd8c555
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362412"
---
# <a name="while"></a>.while


**.While**トークンと同様に動作、**中**C のキーワード

```dbgcmd
.while (Condition) { Commands } 
```

## <a name="span-idddktokenwhiledbgspanspan-idddktokenwhiledbgspansyntax-elements"></a><span id="ddk_token_while_dbg"></span><span id="DDK_TOKEN_WHILE_DBG"></span>構文要素


<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *条件*   
条件を指定します。 これは、0 に評価されると、false; として扱われますそれ以外の場合は true です。 それを囲む*条件*かっこは省略可能です。 *条件*デバッガー コマンドではなく、式を指定する必要があります。 (MASM または C++) の既定式エバリュエーターによって評価されます。 詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *コマンド*   
条件が true、繰り返し実行される 1 つまたは複数のコマンドを指定します。 コマンドのブロックは、1 つのコマンドで構成されている場合でも、中かっこで囲む必要があります。 複数のコマンドは、前に、右中かっこは、セミコロンの後に指定する必要はありませんが、セミコロンで、最後のコマンドで区切る必要があります。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>コメント
-------

[ **.Break** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/-break)と[ **.continue** ](-continue.md)を終了または再起動のトークンを使用できます、*コマンド*ブロックします。

 

 





