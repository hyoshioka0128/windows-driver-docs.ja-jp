---
title: .do
description: 元のトークンは、条件の前に"while"という語が設定されていないことを除いて、C では、do キーワードのように動作します。
ms.assetid: 254413bd-7fa5-4401-b242-470f9c0cf11a
keywords:
- 元の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .do
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fba2b38421d880bb4c051396769a5c7a0877a2f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573266"
---
# <a name="do"></a>.do


**同じ操作を行います**トークンと同様に動作、**は**キーワードは C では、条件の前に"while"という語が設定されていない点が異なります。

```dbgcmd
.do { Commands } (Condition) 
```

## <a name="span-idddktokendodbgspanspan-idddktokendodbgspansyntax-elements"></a><span id="ddk_token_do_dbg"></span><span id="DDK_TOKEN_DO_DBG"></span>構文要素


<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *コマンド*   
条件が true の場合--が常に少なくとも 1 回実行される限り繰り返し実行される 1 つまたは複数のコマンドを指定します。 コマンドのブロックは、1 つのコマンドで構成されている場合でも、中かっこで囲む必要があります。 複数のコマンドは、前に、右中かっこは、セミコロンの後に指定する必要はありませんが、セミコロンで、最後のコマンドで区切る必要があります。

<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *条件*   
条件を指定します。 これは、0 に評価されると、false; として扱われますそれ以外の場合は true です。 それを囲む*条件*かっこは省略可能です。 *条件*デバッガー コマンドではなく、式を指定する必要があります。 (MASM または C++) の既定式エバリュエーターによって評価されます。 詳細については、[数値式の構文](numerical-expression-syntax.md)を参照してください。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)を参照してください。

<a name="remarks"></a>コメント
-------

[ **.Break** ](https://msdn.microsoft.com/library/windows/hardware/ff556242)と[ **.continue** ](-continue.md)を終了または再起動のトークンを使用できます、*コマンド*ブロックします。

 

 





