---
title: amli デバッガー
description: Amli デバッガー拡張機能は、AMLI デバッガーを中断します。
ms.assetid: ef55a45f-445a-4b05-a2a9-b21be3667ec3
keywords:
- Windows デバッグ amli デバッガー
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli debugger
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4240f325201318ad8c90aa393544b89e16f8be2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581809"
---
# <a name="amli-debugger"></a>!amli debugger


**! Amli デバッガー**拡張機能が AMLI デバッガーを中断します。

構文

```dbgcmd
    !amli debugger
```

## <span id="ddk__amli_debugger_dbg"></span><span id="DDK__AMLI_DEBUGGER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>コメント
-------

このコマンドが発行されたときに、通知は、AML インタープリターに送信されます。 すぐに中断 AMLI デバッガーにされる、インタープリターがアクティブで、[次へ] の時刻。

**! Amli デバッガー** 1 つの中断が拡張機能でのみ発生します。 再度中断させる場合は、この拡張機能を使用して、もう一度、または、ブレークポイントを設定する必要があります。

 

 





