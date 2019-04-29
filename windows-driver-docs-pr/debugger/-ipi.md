---
title: ipi
description: Ipi 拡張機能では、指定されたプロセッサのさせるプロセス間割り込み (IPI) の状態を表示します。
ms.assetid: 2727d429-82f5-44a6-943b-0a3f2d3385a3
keywords:
- IPI (させるプロセス間割り込み)
- Windows デバッグ ipi
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ipi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 44ebc77341bacc9f3a67a9fe968686c835d1a6b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336400"
---
# <a name="ipi"></a>!ipi


**! Ipi**拡張機能には、指定されたプロセッサのさせるプロセス間割り込み (IPI) の状態が表示されます。

```dbgcmd
!ipi [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
プロセッサを指定します。 場合*プロセッサ*は省略すると、各プロセッサの IPI 状態が表示されます。

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

 

この拡張機能のコマンドは、x86 ベースの移行先のコンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Ipi については、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

この拡張機能からの出力の例を次に示します。

```dbgcmd
0: kd> !ipi
IPI State for Processor 0
  Worker Routine:  nt!KiFlushTargetMultipleTb [Stale]
  Parameter[0]:    0
  Parameter[1]:    3
  Parameter[2]:    F7C98770
  Ipi Trap Frame:  F7CCCCDC [.trap F7CCCCDC]
  Signal Done:     0
  IPI Frozen:      24 [FreezeActive] [Owner]
  Request Summary: 0
  Target Set:      0
  Packet Barrier:  0

IPI State for Processor 1
  Worker Routine:  nt!KiFlushTargetMultipleTb [Stale]
  Parameter[0]:    1
  Parameter[1]:    3
  Parameter[2]:    F7CDCD28
  Ipi Trap Frame:  F7C8CCC4 [.trap F7C8CCC4]
  Signal Done:     0
  IPI Frozen:      2 [Frozen]
  Request Summary: 0
  Target Set:      0
  Packet Barrier:  0
```

 

 





