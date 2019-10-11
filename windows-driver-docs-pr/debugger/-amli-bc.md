---
title: amli bc
description: Amli bc 拡張機能は、AML ブレークポイントを完全にクリアします。
ms.assetid: e975ee10-cd2f-4944-8d00-b2eda2dd099a
keywords:
- amli bc Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli bc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 16599d6b8c2056b6f83299037d8e413033182aae
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038069"
---
# <a name="amli-bc"></a>!amli bc

**! Amli bc**拡張機能は、AML ブレークポイントを完全にクリアします。

構文

```dbgcmd
    !amli bc Breakpoint
    !amli bc *
```

## <a name="span-idddk__amli_bc_dbgspanspan-idddk__amli_bc_dbgspanparameters"></a><span id="ddk__amli_bc_dbg"></span><span id="DDK__AMLI_BC_DBG"></span>パラメータ

<span id="_______Breakpoint______"></span><span id="_______breakpoint______"></span><span id="_______BREAKPOINT______"></span>*ブレークポイント*消去するブレークポイントの番号を指定します。

<span id="______________"></span> **\*** すべてのブレークポイントをクリアする必要があることを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts .dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途の詳細については、「 [AMLI デバッガー](the-amli-debugger.md)」を参照してください。

<a name="remarks"></a>コメント
-------

ブレークポイントのブレークポイント番号を確認するには、 [ **! amli bl**](-amli-bl.md)拡張機能を使用します。
