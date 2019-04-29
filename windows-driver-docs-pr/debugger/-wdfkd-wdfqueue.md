---
title: wdfkd.wdfqueue
description: Wdfkd.wdfqueue 拡張機能では、指定のフレームワークのキュー オブジェクトと、キューに入っている framework 要求オブジェクトに関する情報が表示されます。
ms.assetid: 100917dc-9ce9-48d6-a285-58ea78a4c2f4
keywords:
- デバッグ wdfkd.wdfqueue Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e1d481c4c9efa1ae1017d601c3d14c8d635a9be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323234"
---
# <a name="wdfkdwdfqueue"></a>!wdfkd.wdfqueue


**! Wdfkd.wdfqueue**拡張機能には、指定のフレームワークのキュー オブジェクトと、キューに入っている framework 要求オブジェクトに関する情報が表示されます。

```dbgcmd
!wdfkd.wdfqueue Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
フレームワークのキュー オブジェクトへのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

次の例は、表示から、 **! wdfkd.wdfqueue**拡張機能。

```dbgcmd
kd> !wdfqueue 0x7ce7d1e8 

# Dumping WDFQUEUE 0x7ce7d1e8
=========================
Parallel, Power-managed, PowerOff, Can accept, Can dispatch, ExecutionLevelDispatch, SynchronizationScopeNone
    Number of driver owned requests: 0
    Number of waiting requests: 0


    EvtIoDefault: (0xf221fad0) wdfrawbusenumtest!EvtIoQueueDefault
```

上記の例では、キューの並列ディスパッチ用に構成されて、電源管理がオフの状態では現在、および両方を受け入れ、要求をディスパッチします。

 

 





