---
title: amli bd
description: Amli bd 拡張機能は、AML ブレークポイントを一時的に無効にします。
ms.assetid: a7fb4f51-8984-425b-858d-1e1e69825891
keywords:
- amli bd Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 57c93d91a8ea5b94622b02b3bf75351fdad53627
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038039"
---
# <a name="amli-bd"></a>!amli bd

**! Amli bd**拡張機能は、AML ブレークポイントを一時的に無効にします。

構文

```dbgcmd
    !amli bd Breakpoint!amli bd *
```

## <a name="span-idddk__amli_bd_dbgspanspan-idddk__amli_bd_dbgspanparameters"></a><span id="ddk__amli_bd_dbg"></span><span id="DDK__AMLI_BD_DBG"></span>パラメータ

<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span>*ブレークポイント*無効にするブレークポイントの番号を指定します。

<span id="______________"></span> **\*** すべてのブレークポイントを無効にすることを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts .dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途の詳細については、「 [AMLI デバッガー](the-amli-debugger.md)」を参照してください。

<a name="remarks"></a>コメント
-------

無効なブレークポイントは、 [ **! amli be**](-amli-be.md)拡張機能を使用して再度有効にすることができます。

ブレークポイントのブレークポイント番号を確認するには、 [ **! amli bl**](-amli-bl.md)拡張機能を使用します。

このコマンドの例を次に示します。

```console
kd> !amli bl
 0:  c29accf5 [\_WAK]
 1:  c29c20a5 [\_SB.PCI0.ISA.BAT1._BST]

kd> !amli bd 1
```
