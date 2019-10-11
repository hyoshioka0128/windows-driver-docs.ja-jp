---
title: amli be
description: Amli be 拡張機能を使用すると、AML ブレークポイントが有効になります。
ms.assetid: 75c0c05f-8c56-4489-a798-2e5ec6ca26d8
keywords:
- amli be Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli be
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a32c06d0706bd16a260b09d86f33ede99c0f327e
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038027"
---
# <a name="amli-be"></a>!amli be

**! Amli be**拡張機能を使用すると、AML ブレークポイントが有効になります。

構文

```dbgcmd
    !amli be Breakpoint!amli be *
```

## <a name="span-idddk__amli_be_dbgspanspan-idddk__amli_be_dbgspanparameters"></a><span id="ddk__amli_be_dbg"></span><span id="DDK__AMLI_BE_DBG"></span>パラメータ

<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span>*ブレークポイント*有効にするブレークポイントのブレークポイント番号を指定します。

<span id="______________"></span> **\*** すべてのブレークポイントを有効にする必要があることを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts .dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途の詳細については、「 [AMLI デバッガー](the-amli-debugger.md)」を参照してください。

<a name="remarks"></a>コメント
-------

すべてのブレークポイントは、作成時に有効になります。 [ **! Amli bd**](-amli-bd.md)拡張機能を使用した場合にのみ、ブレークポイントが無効になります。

ブレークポイントのブレークポイント番号を確認するには、 [ **! amli bl**](-amli-bl.md)拡張機能を使用します。
