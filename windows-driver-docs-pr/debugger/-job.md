---
title: ジョブ (job)
description: ジョブの拡張機能は、ジョブ オブジェクトを表示します。
ms.assetid: 1fbadcc7-d81b-4cfb-a54a-7843e2f78ea1
keywords:
- Windows デバッグ ジョブ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- job
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6bf7d630b4f0d5367147d1f3d6a18c93a4b3a7ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575034"
---
# <a name="job"></a>!job


**! ジョブ**拡張機能は、ジョブ オブジェクトを表示します。

```dbgcmd
!job [Process [Flags]] 
```

## <a name="span-idddkjobdbgspanspan-idddkjobdbgspanparameters"></a><span id="ddk__job_dbg"></span><span id="DDK__JOB_DBG"></span>パラメーター


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
プロセスまたは関連付けられているジョブ オブジェクトは、調査するスレッドの 16 進数のアドレスを指定します。 これを省略すると、または Windows 2000 の場合) の「-1 に等しくないか (Windows xp とそれ以降)、現在のプロセスに関連付けられているジョブを 0 以下が表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示に含める必要がありますを指定します。 これは、次のビット値のいずれかの合計です。 既定値は 0x1 です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
ジョブの設定および統計情報を含むディスプレイをによりします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
ジョブのすべてのプロセスの一覧が表示をによりします。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ジョブのオブジェクトについては、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>コメント
-------

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !process 52c
Searching for Process with Cid == 52c
PROCESS 8276c550  SessionId: 0  Cid: 052c    Peb: 7ffdf000  ParentCid: 0060
    DirBase: 01289000  ObjectTable: 825f0368  TableSize:  24.
    Image: cmd.exe
    VadRoot 825609e8 Vads 30 Clone 0 Private 77. Modified 0. Locked 0.
    DeviceMap e1733f38
    Token                             e1681610
    ElapsedTime                       0:00:12.0949
    UserTime                          0:00:00.0359
    .....
    CommitCharge                      109
    Job                               8256e1f0

kd> !job 8256e1f0
Job at ffffffff8256e1f0
  TotalPageFaultCount      0
  TotalProcesses           1
  ActiveProcesses          1
  TotalTerminatedProcesses 0
  LimitFlags               0
  MinimumWorkingSetSize    0
  MaximumWorkingSetSize    0
  ActiveProcessLimit       0
  PriorityClass            0
  UIRestrictionsClass      0
  SecurityLimitFlags       0
  Token                    00000000
```

 

 





