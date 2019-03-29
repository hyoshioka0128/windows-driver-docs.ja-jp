---
title: amli r
description: Amli r 拡張機能では、現在のコンテキストまたは指定したコンテキストに関する情報が表示されます。
ms.assetid: 1a8977ed-a420-4f68-8580-8e7446075283
keywords:
- Windows デバッグ amli r
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli r
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 28cb2523213a6987388c93c040a2f260ccb47a2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572890"
---
# <a name="amli-r"></a>!amli r


**! Amli r**拡張機能は、現在のコンテキストまたは指定したコンテキストに関する情報を表示します。

構文

```dbgcmd
   !amli r [ContextAddress]
```

## <a name="span-idddkamlirdbgspanspan-idddkamlirdbgspanparameters"></a><span id="ddk__amli_r_dbg"></span><span id="DDK__AMLI_R_DBG"></span>パラメーター


<span id="_______ContextAddress______"></span><span id="_______contextaddress______"></span><span id="_______CONTEXTADDRESS______"></span> *ContextAddress*   
表示されるコンテキストのブロックのアドレスを指定します。 コンテキストのブロックのアドレスを決定できます、 **Ctxt**フィールドに、 [ **! amli lc** ](-amli-lc.md)を表示します。 場合*ContextAddress*に 2 つのパーセント記号が付いています (**%%**)、物理アドレスとして解釈されます。 それ以外の場合、その仮想アドレスとして解釈されます。 このパラメーターを省略すると、現在のコンテキストが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>コメント
-------

かどうか、AMLI デバッガーが突然プロンプトが表示されたら、これが便利なコマンドを使用します。

たとえば、次のコマンドは、インタープリターの現在のコンテキストに表示されます。

```console
AMLI(? for help)-> r

Context=c18b4000*, Queue=00000000, ResList=00000000
ThreadID=c15a6618, Flags=00000010
StackTop=c18b5eec, UsedStackSize=276 bytes, FreeStackSize=7636 bytes
LocalHeap=c18b40c0, CurrentHeap=c18b40c0, UsedHeapSize=88 bytes
Object=\_WAK, Scope=\_WAK, ObjectOwner=c18b4108, SyncLevel=0
AsyncCallBack=ff06b5d0, CallBackData=0, CallBackContext=c99efddc

MethodObject=\_WAK
80e0ff5c: Local0=Unknown()
80e0ff70: Local1=Unknown()
80e0ff84: Local2=Unknown()
80e0ff98: Local3=Unknown()
80e0ffac: Local4=Unknown()
80e0ffc0: Local5=Unknown()
80e0ffd4: Local6=Unknown()
80e0ffe8: Local7=Unknown()
80e0e040: RetObj=Unknown()

Next AML Pointer: ffffffff80e630df:[\_WAK+16]

ffffffff80e630df : If(S4BW
ffffffff80e630e5 : {
ffffffff80e630e5 : | Store(Zero, S4BW)
ffffffff80e630eb : }
```

 

 





