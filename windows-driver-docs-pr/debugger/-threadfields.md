---
title: threadfields
description: Threadfields 拡張機能では、名前と、executive スレッド (ETHREAD) ブロック内のフィールドのオフセットが表示されます。
ms.assetid: 1b36e922-9079-4dc5-911a-f635ec026084
keywords:
- Windows デバッグ threadfields
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- threadfields
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 83e496d76ee22a7b2cdb1743aaaf3f7a1079701f
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239181"
---
# <a name="threadfields"></a>!threadfields


**! Threadfields**拡張機能は、名前と、executive スレッド (ETHREAD) ブロック内のフィールドのオフセットが表示されます。

```dbgcmd
!threadfields
```

## <span id="ddk__threadfields_dbg"></span><span id="DDK__THREADFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>利用不可 (「解説」を参照してください)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ETHREAD ブロックについては、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

この拡張機能のコマンドは、Windows XP または Windows の以降のバージョンでご利用いただけません。 代わりに、使用、 [ **dt (表示の種類)** ](dt--display-type-.md) ETHREAD 構造体を直接表示するコマンド。

```dbgcmd
kd> dt nt!_ETHREAD 
```

次の例に示します **! threadfields** Windows 2000 システムから。

```dbgcmd
kd> !threadfields
 ETHREAD structure offsets:

    Tcb:                           0x0
    CreateTime:                    0x1b0
    ExitTime:                      0x1b8
    ExitStatus:                    0x1c0
    PostBlockList:                 0x1c4
    TerminationPortList:           0x1cc
    ActiveTimerListLock:           0x1d4
    ActiveTimerListHead:           0x1d8
    Cid:                           0x1e0
    LpcReplySemaphore:             0x1e8
    LpcReplyMessage:               0x1fc
    LpcReplyMessageId:             0x200
    ImpersonationInfo:             0x208
    IrpList:                       0x20c
    TopLevelIrp:                   0x214
    ReadClusterSize:               0x21c
    ForwardClusterOnly:            0x220
    DisablePageFaultClustering:    0x221
    DeadThread:                    0x222
    HasTerminated:                 0x224
    GrantedAccess:                 0x228
    ThreadsProcess:                0x22c
    StartAddress:                  0x230
    Win32StartAddress:             0x234
    LpcExitThreadCalled:           0x238
    HardErrorsAreDisabled:         0x239
```

 

 





