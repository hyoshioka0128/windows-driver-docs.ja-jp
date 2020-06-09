---
title: ucx_controller usb3kd
description: Ucx_controller usb3kd コマンドは、USB 3.0 ホストコントローラーに関する情報を表示します。 表示は、UcxVersion. sys によって管理されるデータ構造に基づいています。
ms.assetid: A2768E47-C8D7-4A01-80AC-98FB5AAA17BD
keywords:
- usb3kd Windows デバッグの ucx_controller
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_controller
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1158ebf742230058be2a4bd2f0524215282d4d8
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534707"
---
# <a name="usb3kducx_controller"></a>! usb3kd \_ コントローラー


[**! Usb3kd \_ controller**](-usb3kd-device-info.md)コマンドは、USB 3.0 ホストコントローラーに関する情報を表示します。 この表示は、USB ホストコントローラー拡張機能ドライバー (Ucx*バージョン*.sys) によって管理されるデータ構造に基づいています。

```dbgcmd
!usb3kd.ucx_controller UcxControllerPrivContext
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______UcxControllerPrivContext______"></span><span id="_______ucxcontrollerprivcontext______"></span><span id="_______UCXCONTROLLERPRIVCONTEXT______"></span>*Ucxコントローラーのプライベートコンテキスト*   
\_コントローラーを表す ucxcontroller \_ privcontext 構造体のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

Usb ホストコントローラー拡張機能ドライバー (Ucx*バージョン*.sys) は、usb 3.0 ハブドライバーと usb 3.0 ホストコントローラードライバーの間に抽象層を提供します。 拡張機能ドライバーは、ホストコントローラー、デバイス、およびエンドポイントを独自に表現したものです。 出力[**! ucx \_ controller**](-usb3kd-device-info.md)コマンドは、拡張機能ドライバーによって保持されているデータ構造に基づいています。 Usb ホストコントローラー拡張機能ドライバーおよび USB 3.0 ホストコントローラードライバーの詳細については、「 [Usb ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

<a name="examples"></a>例
--------

UCX コントローラーのプライベートコンテキストのアドレスを取得するには、 [**! ucx \_ コントローラー \_ リスト**](-usb3kd-ucx-controller-list.md)コマンドの出力を確認します。 次の例では、プライベートコンテキストのアドレスは0xfffffa80052da050 です。

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

これで、UCX コントローラーのプライベートコンテキストのアドレスを[**! ucx \_ コントローラー**](-usb3kd-device-info.md)コマンドに渡すことができるようになりました。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! usb3kd \_ コントローラーの \_ 一覧**](-usb3kd-ucx-controller-list.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






