---
title: amli bd
description: Amli bd 拡張機能には、AML ブレークポイントを一時的に無効にします。
ms.assetid: a7fb4f51-8984-425b-858d-1e1e69825891
keywords:
- Windows デバッグ amli bd
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba99828d281e9ec87561bd1aa9860faf5c84de32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334779"
---
# <a name="amli-bd"></a>!amli bd


**! Amli bd**拡張機能には、AML ブレークポイントを一時的に無効にします。

構文

```dbgcmd
    !amli bd Breakpoint!amli bd *
```

## <a name="span-idddkamlibddbgspanspan-idddkamlibddbgspanparameters"></a><span id="ddk__amli_bd_dbg"></span><span id="DDK__AMLI_BD_DBG"></span>パラメーター


<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span> *ブレークポイント*   
無効にするブレークポイントの数を指定します。

<span id="______________"></span> **\\***   
すべてのブレークポイントを無効にすることを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>注釈
-------

使用して無効になっているブレークポイントが再度有効にできますが、 [ **! amli する**](-amli-be.md)拡張機能。

ブレークポイントのブレークポイントの数を調べるには、 [ **! amli bl** ](-amli-bl.md)拡張機能。

このコマンドの例を次に示します。

```console
kd> !amli bl
 0:  c29accf5 [\_WAK]
 1:  c29c20a5 [\_SB.PCI0.ISA.BAT1._BST]

kd> !amli bd 1
```

 

 





