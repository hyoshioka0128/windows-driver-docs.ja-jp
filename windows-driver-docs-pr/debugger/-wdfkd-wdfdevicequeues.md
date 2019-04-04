---
title: wdfkd.wdfdevicequeues
description: Wdfkd.wdfdevicequeues 拡張機能では、指定されたデバイスに属しているフレームワークのキュー オブジェクトのすべてに関する情報が表示されます。
ms.assetid: bd0e7fcc-b561-48fb-901a-605e9d647b61
keywords:
- デバッグ wdfkd.wdfdevicequeues Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdevicequeues
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d46ae2fe52473f64845d16191813a91c62e35fff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580354"
---
# <a name="wdfkdwdfdevicequeues"></a>!wdfkd.wdfdevicequeues


**! Wdfkd.wdfdevicequeues**拡張機能は、すべての指定したデバイスに属しているフレームワークのキュー オブジェクトに関する情報を表示します。

```dbgcmd
!wdfkd.wdfdevicequeues Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
WDFDEVICE に型指定されたオブジェクトへのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)と[ **! wdfkd.wdfqueue**](-wdfkd-wdfqueue.md)を参照してください。

<a name="remarks"></a>コメント
-------

次の例は、表示から、 **! wdfkd.wdfdevicequeues**拡張機能。

```dbgcmd
kd> !wdfdevicequeues 0x7cad31c8 

# Dumping queues of WDFDEVICE 0x7cad31c8
=====================================
## Number of queues: 3
----------------------------------
Queue: 1 (!wdfqueue 0x7d67d1e8)
    Manual, Not power-managed, PowerOn, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


## This is WDF internal queue for create requests.
----------------------------------
Queue: 2 (!wdfqueue 0x7ce7d1e8)
    Parallel, Power-managed, PowerOff, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


##     EvtIoDefault: (0xf221fad0) wdfrawbusenumtest!EvtIoQueueDefault
----------------------------------
Queue: 3 (!wdfqueue 0x7cd671e8)
    Parallel, Power-managed, PowerOff, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


    EvtIoDeviceControl: (0xf2226ac0) wdfrawbusenumtest!RawBus_RawPdo_EvtDeviceControl
```

 

 





