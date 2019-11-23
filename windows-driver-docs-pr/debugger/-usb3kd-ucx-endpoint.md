---
title: ucx_endpoint usb3kd
description: Usb3kd コマンドは、usb 3.0 ツリーの USB デバイスのエンドポイントに関する情報を表示し ucx_endpoint ます。 表示は、UcxVersion. sys によって保持されているデータに基づいています。
ms.assetid: 37667665-ACA1-48D3-B79E-5B9BBD689034
keywords:
- usb3kd Windows デバッグの ucx_endpoint
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_endpoint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 31f067172eb8e297d45292ffc5da977772566254
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837839"
---
# <a name="usb3kducx_endpoint"></a>! usb3kd\_エンドポイント


[ **! Usb3kd\_endpoint**](-usb3kd-device-info.md)コマンドは、usb [3.0 ツリー](usb-3-extensions.md#usb-3-tree)の usb デバイス上のエンドポイントに関する情報を表示します。 この表示は、USB ホストコントローラー拡張機能ドライバー (Ucx*バージョン*.sys) によって管理されるデータ構造に基づいています。

```dbgcmd
!usb3kd.ucx_endpoint UcxEndpointPrivContext
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______UcxEndpointPrivContext______"></span><span id="_______ucxendpointprivcontext______"></span><span id="_______UCXENDPOINTPRIVCONTEXT______"></span>*Ucxendpointprivcontext*   
エンドポイントを表す \_UCXENDPOINT\_PRIVCONTEXT 構造体のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

Usb ホストコントローラー拡張機能ドライバー (Ucx*バージョン*.sys) は、usb 3.0 ハブドライバーと usb 3.0 ホストコントローラードライバーの間に抽象層を提供します。 拡張機能ドライバーは、ホストコントローラー、デバイス、およびエンドポイントを独自に表現したものです。 **! Ucx\_endpoint**コマンドの出力は、拡張機能ドライバーによって保持されているデータ構造に基づいています。 Usb ホストコントローラー拡張機能ドライバーおよび USB 3.0 ホストコントローラードライバーの詳細については、「 [Usb ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

<a name="examples"></a>例
--------

UCX エンドポイントのプライベートコンテキストのアドレスを取得するには、 [ **! ucx\_controller\_list**](-usb3kd-ucx-controller-list.md)コマンドの出力を確認します。 次の例では、2番目のデバイスの最初のエンドポイントのプライベートコンテキストのアドレスは0xfffffa8003694860 です。

```dbgcmd
3: kd> !ucx_controller_list

## Dumping List of UCX controller objects
--------------------------------------
[1] !ucx_controller 0xfffffa80052da050 (dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT fffffa80052da050)
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

これで、UCX エンドポイントのプライベートコンテキストのアドレスを **! ucx\_endpoint**コマンドに渡すことができるようになりました。

```dbgcmd
3: kd> !ucx_endpoint 0xfffffa8003694860

## Dumping Ucx USB Endpoint Information fffffa8003694860
-----------------------------------------------------
dt ucx01000!_UCXENDPOINT_PRIVCONTEXT 0xfffffa8003694860
[Blk Out], UcxEndpointStateEnabled, MaxTransferSize: 4194304
Endpoint Address: 0x02
Endpoint Queue: !wdfqueue 0x57ffc969888

UcxEndpoint State History: <Event> NewState 
    [ 3] <UcxEndpointEventOperationSuccess> UcxEndpointStateEnabled
    [ 2] <UcxEndpointEventYes> UcxEndpointStateCompletingPendingOperation1
    [ 1] <UcxEndpointEventEnableComplete> UcxEndpointStateIsAbleToStart2
    [ 0] <SmEngineEventStart> UcxEndpointStateCreated

UcxEndpoint Event History:
    [ 1] UcxEndpointEventEnableComplete
    [ 0] SmEngineEventStart

EventCallbacks:
    EvtEndpointPurge: (0xfffff880044ba6e8) USBXHCI!Endpoint_UcxEvtEndpointPurge
    EvtEndpointAbort: (0xfffff880044ba94c) USBXHCI!Endpoint_UcxEvtEndpointAbort
    EvtEndpointReset: (0xfffff880044bb854) USBXHCI!Endpoint_UcxEvtEndpointReset
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[ **! usb3kd\_controller\_list**](-usb3kd-ucx-controller-list.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






