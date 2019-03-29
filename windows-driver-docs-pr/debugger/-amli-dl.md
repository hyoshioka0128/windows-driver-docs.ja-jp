---
title: amli dl
description: Amli dl の拡張機能では、AML インタープリターのイベント ログの一部が表示されます。
ms.assetid: 06565760-d7f0-4f22-8670-7706d3b4b3a8
keywords:
- Windows デバッグ amli dl
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli dl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56c2f0b89dec17c254db3b7ee04faee5f14586f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578246"
---
# <a name="amli-dl"></a>!amli dl


**! Amli dl**拡張機能には、AML インタープリターのイベント ログの一部が表示されます。

構文

```dbgcmd
    !amli dl
```

## <span id="ddk__amli_dl_dbg"></span><span id="DDK__AMLI_DL_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>コメント
-------

イベント ログは、インタープリターで発生した最新の 150 イベントを記録します。

ログの表示の例を次に示します。

```console
kd> !amli dl
RUN!: [c15a6618]QTh=00000000,QCt=00000000,QFg=00000000: Ctx=c18b4000,rc=0
KICK: [c15a6618]QTh=00000000,QCt=00000000,QFg=00000000: rc=0
SYNC: [c15a6618]QTh=00000000,QCt=00000000,QFg=00000002,LockPhase=0,Locked=0,IRQL=00: Obj=\_WAK
ASYN: [c15a6618]QTh=00000000,QCt=00000000,QFg=00000002,LockPhase=0,Locked=0,IRQL=00: Obj=\_WAK
REST: [c15a6618]QTh=00000000,QCt=00000000,QFg=00000002: Ctx=c18b4000,Obj=\_WAK
INSQ: [c15a6618]QTh=00000000,QCt=00000000,QFg=00000002: Ctx=c18b4000,Obj=\_WAK
EVAL: [c15a6618]QTh=00000000,QCt=00000000,QFg=00000002: Ctx=c18b4000,Obj=\_WAK
RUNC: [c15a6618]QTh=c15a6618,QCt=c18b4000,QFg=00000002: Ctx=c18b4000,Obj=\_WAK
```

 

 





