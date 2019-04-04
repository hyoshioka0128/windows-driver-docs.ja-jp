---
title: usb3kd.ucx_controller
description: Usb3kd.ucx_controller コマンドでは、USB 3.0 ホスト コント ローラーに関する情報が表示されます。 表示は、UcxVersion.sys によって管理されるデータ構造に基づいています。
ms.assetid: A2768E47-C8D7-4A01-80AC-98FB5AAA17BD
keywords:
- デバッグ usb3kd.ucx_controller Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_controller
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e2afdca1987dad0b12a4636412cf6f2afcbf9105
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573982"
---
# <a name="usb3kducxcontroller"></a>!usb3kd.ucx\_controller


[ **! Usb3kd.ucx\_コント ローラー** ](-usb3kd-device-info.md)コマンドは、USB 3.0 ホスト コント ローラーに関する情報を表示します。 USB ホスト コント ローラーの拡張機能ドライバーによって管理されるデータ構造に基づいて表示 (Ucx*バージョン*.sys)。

```dbgcmd
!usb3kd.ucx_controller UcxControllerPrivContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______UcxControllerPrivContext______"></span><span id="_______ucxcontrollerprivcontext______"></span><span id="_______UCXCONTROLLERPRIVCONTEXT______"></span> *UcxControllerPrivContext*   
アドレス、 \_UCXCONTROLLER\_コント ローラーを表す PRIVCONTEXT 構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>コメント
-------

USB ホスト コント ローラーの拡張機能ドライバー (Ucx*バージョン*.sys) コント ローラーのドライバーの USB 3.0 ハブのドライバーと USB 3.0 ホスト間の抽象化レイヤーを提供します。 拡張機能ドライバーが、ホスト コント ローラー、デバイス、およびエンドポイントの独自の表現。 出力、 [ **! ucx\_コント ローラー** ](-usb3kd-device-info.md)コマンドは、拡張機能ドライバーによって管理されるデータ構造に基づきます。 USB ホスト コント ローラーの拡張機能ドライバーと USB 3.0 ホスト コント ローラーのドライバーの詳細については、[USB ドライバー スタック アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/hh406256)を参照してください。

<a name="examples"></a>使用例
--------

UCX コント ローラーのプライベート コンテキストのアドレスを取得する出力の確認、 [ **! ucx\_コント ローラー\_一覧**](-usb3kd-ucx-controller-list.md)コマンド。 次の例では、プライベート コンテキストのアドレスは、0xfffffa80052da050 です。

```dbgcmd
3: kd> !ucx_controller_list

## Dumping List of UCX controller objects
--------------------------------------
[1] !ucx_controller 0xfffffa80052da050 (dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT fffffa80052da050)
    !ucx_device 0xfffffa8005a41840
        .!ucx_endpoint 0xfffffa800533f3d0 [Blk In ], UcxEndpointStateEnabled
        ...
    !ucx_device 0xfffffa8005bd9680
        .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
        ...
```

UCX コント ローラーのプライベート コンテキストへのアドレスを渡すことができますので、 [ **! ucx\_コント ローラー** ](-usb3kd-device-info.md)コマンド。

```dbgcmd
3: kd> !ucx_controller 0xfffffa80052da050

## Dumping Ucx Controller Information fffffa80052da050
---------------------------------------------------
dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT 0xfffffa80052da050
Parent Device: !wdfdevice 0x57ffac91fd8
Controller Queues:
    Default               : !wdfqueue 0x57ffacc5fd8
    Address'0'Ownership   : !wdfqueue 0x57ffad5ad88
    DeviceManagement      : !wdfqueue 0x57ffacd6fd8
    ... pend on Ctrl Reset: !wdfqueue 0x57ffad48fd8

Controller Reset State History: <Event> NewState 
    [ 2] <ControllerResetEventOperationSuccess> ControllerResetStateRHPdoInD0
    [ 1] <ControllerResetEventRHPdoEnteredD0> ControllerResetStateStopBlockingResetComplete1
    [ 0] <SmEngineEventStart> ControllerResetStateRhPdoInDx

Controller Reset Event History:
    [ 1] ControllerResetEventRHPdoEnteredD0
    [ 0] SmEngineEventStart

Root Hub PDO: !wdfdevice 0x57ffaf4daa8
Number of 2.0 Ports: 2
Number of 3.0 Ports: 2
RootHub Control !wdfqueue 0x57ffacb4798
RootHub Interrupt !wdfqueue 0x57ffad033f8, pending !wdfequest 0x57ffa5fe998

Device Tree:
    !ucx_device 0xfffffa8005a41840
        .!ucx_endpoint 0xfffffa800533f3d0 [Blk In ], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa80053405d0 [Blk Out], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005a3f710 [Control], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005bbe4e0 [Blk Out], UcxEndpointStateStale
        .!ucx_endpoint 0xfffffa8005ac4810 [Blk In ], UcxEndpointStateStale
    !ucx_device 0xfffffa8005bd9680
        .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8003686820 [Blk In ], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005be0550 [Control], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8003695580 [Blk In ], UcxEndpointStateStale
        .!ucx_endpoint 0xfffffa80036a20c0 [Blk Out], UcxEndpointStateStale
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! usb3kd.ucx\_コント ローラー\_一覧**](-usb3kd-ucx-controller-list.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






