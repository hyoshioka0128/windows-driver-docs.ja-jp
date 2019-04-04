---
title: amli します。
description: 拡張機能により、AML ブレークポイントを amli にあります。
ms.assetid: 75c0c05f-8c56-4489-a798-2e5ec6ca26d8
keywords:
- amli する Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli be
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc978d103915560d5fd62f111678fe43645bb97c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548594"
---
# <a name="amli-be"></a>! amli します。


**! Amli する**拡張機能により、AML ブレークポイント。

構文

```dbgcmd
    !amli be Breakpoint!amli be *
```

## <a name="span-idddkamlibedbgspanspan-idddkamlibedbgspanparameters"></a><span id="ddk__amli_be_dbg"></span><span id="DDK__AMLI_BE_DBG"></span>パラメーター


<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span> *ブレークポイント*   
ブレークポイントの数を有効にするブレークポイントを指定します。

<span id="______________"></span> **\\***   
すべてのブレークポイントを有効にすることを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、[AMLI デバッガー](the-amli-debugger.md)を参照してください。

<a name="remarks"></a>注釈
-------

作成されるときに、すべてのブレークポイントが有効にします。 使用した場合、ブレークポイントを無効にのみ、 [ **! amli bd** ](-amli-bd.md)拡張機能。

ブレークポイントのブレークポイントの数を調べるには、 [ **! amli bl** ](-amli-bl.md)拡張機能。

 

 





