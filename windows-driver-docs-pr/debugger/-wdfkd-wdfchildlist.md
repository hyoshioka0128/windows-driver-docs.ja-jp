---
title: wdfkd.wdfchildlist
description: Wdfkd.wdfchildlist 拡張機能には、子リストの状態とすべての子リスト内にあるデバイスの識別の説明に関する情報が表示されます。
ms.assetid: b224e898-0e49-431e-a748-ea12ff3b3513
keywords:
- デバッグ wdfkd.wdfchildlist Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfchildlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 052f849b144e2ce920c09b7e0442b346222bee98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341792"
---
# <a name="wdfkdwdfchildlist"></a>!wdfkd.wdfchildlist


**! Wdfkd.wdfchildlist**拡張機能は、子リストの状態とすべての子リスト内にあるデバイスの識別の説明に関する情報が表示されます。

```dbgcmd
!wdfkd.wdfchildlist Handle 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
子リストに WDFCHILDLIST に型指定されたハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

次の例は、 **! wdfkd.wdfchildlist**を表示します。

```dbgcmd
kd> !wdfchildlist 0x7cc090c8 

## Dumping WDFCHILDLIST 0x7cc090c8
---------------------------------------
owning !WDFDEVICE 0x7ca7b1c0
ID description size 0x8

State:
-----
List is unlocked, changes will be applied immediately
No scans or enumerations are active on the list

Descriptions:
------------
 PDO !WDFDEVICE 0x7cad31c8, ID description 0x83ac4ff4
 +Device WDM !devobj 0x81fb00e8, WDF pnp state WdfDevStatePnpStarted (0x119)
 +Device found in last scan

No pending insertions are in the list.

Callbacks:
---------
 EvtChildListCreateDevice:  wdfrawbusenumtest!RawBus_RawPdo_Create (f22263b0)
```

 

 





