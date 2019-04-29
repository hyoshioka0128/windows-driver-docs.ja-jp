---
title: iovirp
description: Iovirp 拡張機能では、指定した I/O Verifier IRP の詳細情報が表示されます。
ms.assetid: 9b05061c-2a57-4e01-bbe0-2e2f5f676947
keywords:
- I/O の検証方法
- Windows デバッグ iovirp
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- iovirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27248b4fa1cee453f8bf9c7d33092688d5aec5ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336408"
---
# <a name="iovirp"></a>!iovirp


**! Iovirp**拡張機能には、指定した I/O Verifier IRP の詳細情報が表示されます。

```dbgcmd
!iovirp [IRP]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______IRP______"></span><span id="_______irp______"></span> *IRP*   
Driver Verifier によって追跡 IRP のアドレスを指定します。 場合*IRP*は 0 です。 または、省略すると、各未処理 IRP の概要情報が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !iovirp 947cef68
IovPacket       84509af0
TrackedIrp      947cef68
HeaderLock      84509d61
LockIrql        0
ReferenceCount  1
PointerCount    1
HeaderFlags     00000000
ChainHead       84509af0
Flags           00200009
DepartureIrql   0
ArrivalIrql     0
StackCount      1
QuotaCharge     00000000
QuotaProcess    0
RealIrpCompletionRoutine        0
RealIrpControl                  0
RealIrpContext                  0
TopStackLocation        2
PriorityBoost           0
LastLocation            0
RefTrackingCount        0
SystemDestVA            0
VerifierSettings        84509d08
pIovSessionData         84509380
Allocation Stack:
  nt!IovAllocateIrp+1a  (817df356)
 nt!IopXxxControlFile+40c  (8162de20)
  nt!NtDeviceIoControlFile+2a  (81633090)
 nt!KiFastCallEntry+164  (81513c64)
  nt!EtwpFlushBuffer+10f  (817606d7)
  nt!EtwpFlushBuffersWithMarker+bd  (817608cb)
  nt!EtwpFlushActiveBuffers+2b4  (81760bc2)
  nt!EtwpLogger+213  (8176036f)
```

任意の時点での実行を停止するには、CTRL + BREAK (WinDbg) で、または (KD) では、CTRL + C キーを押します。

 

 





