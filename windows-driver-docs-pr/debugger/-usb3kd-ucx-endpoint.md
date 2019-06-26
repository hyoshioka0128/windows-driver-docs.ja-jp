---
title: usb3kd.ucx_endpoint
description: Usb3kd.ucx_endpoint コマンドでは、USB 3.0 ツリー内の USB デバイスをエンドポイントに関する情報が表示されます。 表示は、UcxVersion.sys によって維持されるデータに基づきます。
ms.assetid: 37667665-ACA1-48D3-B79E-5B9BBD689034
keywords:
- デバッグ usb3kd.ucx_endpoint Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_endpoint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6ac241bdc8e19e08be992c6bf79f78d782a02050
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359779"
---
# <a name="usb3kducxendpoint"></a>!usb3kd.ucx\_endpoint


[ **! Usb3kd.ucx\_エンドポイント**](-usb3kd-device-info.md)コマンドは、USB デバイスで、エンドポイントに関する情報を表示、 [USB 3.0 ツリー](usb-3-extensions.md#usb-3-tree)します。 USB ホスト コント ローラーの拡張機能ドライバーによって管理されるデータ構造に基づいて表示 (Ucx*バージョン*.sys)。

```dbgcmd
!usb3kd.ucx_endpoint UcxEndpointPrivContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______UcxEndpointPrivContext______"></span><span id="_______ucxendpointprivcontext______"></span><span id="_______UCXENDPOINTPRIVCONTEXT______"></span> *UcxEndpointPrivContext*   
アドレス、 \_UCXENDPOINT\_エンドポイントを表す PRIVCONTEXT 構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

USB ホスト コント ローラーの拡張機能ドライバー (Ucx*バージョン*.sys) コント ローラーのドライバーの USB 3.0 ハブのドライバーと USB 3.0 ホスト間の抽象化レイヤーを提供します。 拡張機能ドライバーが、ホスト コント ローラー、デバイス、およびエンドポイントの独自の表現。 出力、 **! ucx\_エンドポイント**コマンドは、拡張機能ドライバーによって管理されるデータ構造に基づきます。 USB ホスト コント ローラーの拡張機能ドライバーと USB 3.0 ホスト コント ローラーのドライバーの詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

<a name="examples"></a>例
--------

UCX エンドポイントのプライベート コンテキストのアドレスを取得する出力の確認、 [ **! ucx\_コント ローラー\_一覧**](-usb3kd-ucx-controller-list.md)コマンド。 次の例では、2 つ目のデバイス上の最初のエンドポイントのプライベート コンテキストのアドレスは、0xfffffa8003694860 です。

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

UCX エンドポイントのプライベート コンテキストへのアドレスを渡すことができますので、 **! ucx\_エンドポイント**コマンド。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[ **! usb3kd.ucx\_コント ローラー\_一覧**](-usb3kd-ucx-controller-list.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






