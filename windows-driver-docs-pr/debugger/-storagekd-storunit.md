---
title: storagekd.storunit
description: Storagekd.storunit 拡張機能は、指定された、Storport の論理ユニット情報を表示します。
ms.assetid: 73A2632C-962E-4075-97B9-5D7D843E9D0F
keywords:
- デバッグ storagekd.storunit Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storunit
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3cc7d844b0cae7c1ebaa2dc2cd3c1c6280722495
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572468"
---
# <a name="storagekdstorunit"></a>!storagekd.storunit


**! Storagekd.storunit**拡張機能は、指定された、Storport の論理ユニットに関する情報を表示します。

```dbgcmd
!storagekd.storunit [Address] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address"></span><span id="_______address"></span><span id="_______ADDRESS"></span> *アドレス*  
Storport 単位のデバイス オブジェクトのアドレスを指定します。 場合*アドレス*は省略すると、Storport のすべてのユニットの一覧が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 以降</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

次の例に示します、 **! storagekd.storunit**表示。

**0: kd&gt; !storagekd.storunit**

```dbgcmd
# STORPORT Units:
==================
## Product                 SCSI ID  Object            Extension         Pnd Out Ct  State
--------------------------------------------------------------------------------------
Msft       Virtual Di   0  0  1  fffffa800658a060  fffffa800658a1b0    0   0  0  Working
```

**0: kd&gt; !storagekd.storunit fffffa800658a060**

```dbgcmd
   DO fffffa800658a060   Ext fffffa800658a1b0   Adapter fffffa800649a1a0   Working
   Vendor: Msft       Product: Virtual Disk       SCSI ID: (0, 0, 1)   
   Claimed Enumerated 
   SlowLock Free   RemLock 1   PageCount 0
   QueueTagList: fffffa800658a270      Outstanding: Head fffffa800658a398  Tail fffffa800658a398  Timeout -1
   DeviceQueue fffffa800658a2a0   Depth: 250   Status: Not Frozen   PauseCount: 0   BusyCount: 0   
   IO Gateway: Busy Count 0   Pause Count 0
   Requests: Outstanding 0   Device 0   ByPass 0


[Device-Queued Requests]

## IRP               SRB Type   SRB               XRB               Command           MDL               SGList            Timeout
-----------------------------------------------------------------------------------------------------------------------------------


[Bypass-Queued Requests]

## IRP               SRB Type   SRB               XRB               Command           MDL               SGList            Timeout
-----------------------------------------------------------------------------------------------------------------------------------


[Outstanding Requests]

## IRP               SRB Type   SRB               XRB               Command           MDL               SGList            Timeout
-----------------------------------------------------------------------------------------------------------------------------------


[Completed Requests]

IRP               SRB Type   SRB               XRB               Command           MDL               SGList            Timeout
-----------------------------------------------------------------------------------------------------------------------------------
```

 

 





