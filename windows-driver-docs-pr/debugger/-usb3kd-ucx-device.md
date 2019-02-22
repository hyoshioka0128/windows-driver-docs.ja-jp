---
title: usb3kd.ucx_device
description: Usb3kd.ucx_device 拡張機能では、USB 3.0 ツリーの中に USB デバイスに関する情報が表示されます。 表示は、UcxVersion.sys によって管理されるデータ構造に基づいています。
ms.assetid: 7AC3DBBF-1D62-492E-B46E-C193579DE1E3
keywords:
- デバッグ usb3kd.ucx_device Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_device
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e531175c38ab20fd474c7f7bef18d2f3ca26e371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556482"
---
# <a name="usb3kducxdevice"></a>!usb3kd.ucx\_device


[ **! Usb3kd.ucx\_デバイス**](-usb3kd-device-info.md)拡張機能での USB デバイスに関する情報を表示する、 [USB 3.0 ツリー](usb-3-extensions.md#usb-3-tree)します。 USB ホスト コント ローラーの拡張機能ドライバーによって管理されるデータ構造に基づいて表示 (Ucx*バージョン*.sys)。

```dbgcmd
!usb3kd.ucx_device UcxUsbDevicePrivContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______UcxUsbDevicePrivContext______"></span><span id="_______ucxusbdeviceprivcontext______"></span><span id="_______UCXUSBDEVICEPRIVCONTEXT______"></span> *UcxUsbDevicePrivContext*   
アドレス、 \_UCXUSBDEVICE\_デバイスを表す PRIVCONTEXT 構造体。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>注釈
-------

USB ホスト コント ローラーの拡張機能ドライバー (Ucx*バージョン*.sys) コント ローラーのドライバーの USB 3.0 ハブのドライバーと USB 3.0 ホスト間の抽象化レイヤーを提供します。 拡張機能ドライバーが、ホスト コント ローラー、デバイス、およびエンドポイントの独自の表現。 出力、 [ **! ucx\_デバイス**](-usb3kd-device-info.md)コマンドは、拡張機能ドライバーによって管理されるデータ構造に基づきます。 USB ホスト コント ローラーの拡張機能ドライバーと USB 3.0 ホスト コント ローラーのドライバーの詳細については、次を参照してください。 [USB ドライバー スタック アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/hh406256)します。

**! ucx\_デバイス**と[ **! デバイス\_情報**](-usb3kd-device-info.md)デバイスに関する情報の両方が表示が表示される情報は異なります。 出力 **! ucx\_デバイス**は USB ホスト コント ローラーの拡張機能ドライバーの point of view およびの出力から **! デバイス\_情報**USB 3.0 ハブの観点からは、ドライバー。 たとえば、 **! ucx\_デバイス**出力には、エンドポイントに関する情報が含まれています、 **! デバイス\_情報**出力には、構成、およびインターフェイスに関する情報が含まれています。記述子。

<a name="examples"></a>例
--------

デバイスのプライベート コンテキスト UCX USB のアドレスを取得する出力の確認、 [ **! ucx\_コント ローラー\_一覧**](-usb3kd-ucx-controller-list.md)コマンド。 次の例では、2 つ目のデバイスのプライベートのコンテキストのアドレスは、0xfffffa8005bd9680 です。

```dbgcmd
3: 3: kd> !ucx_controller_list

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

UCX USB プライベート コンテキストのアドレスを渡すことができますので、 **! ucx\_デバイス**コマンド。

```dbgcmd
3: kd> !ucx_device 0xfffffa8005bd9680

## Dumping Ucx USB Device Information fffffa8005bd9680
---------------------------------------------------
dt ucx01000!_UCXUSBDEVICE_PRIVCONTEXT 0xfffffa8005bd9680
!ucx_controller 0xfffffa80052da050
ParentHub: !wdfhandle 0x57ffacbce78
DefaultEndpoint: !ucx_endpoint 0xfffffa8005be0550
ListOfEndpionts:
    .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
    .!ucx_endpoint 0xfffffa8003686820 [Blk In ], UcxEndpointStateEnabled
    .!ucx_endpoint 0xfffffa8005be0550 [Control], UcxEndpointStateEnabled
    .!ucx_endpoint 0xfffffa8003695580 [Blk In ], UcxEndpointStateStale
    .!ucx_endpoint 0xfffffa80036a20c0 [Blk Out], UcxEndpointStateStale

EventCallbacks:
    EvtUsbDeviceEndpointsConfigure: (0xfffff880044d1164) USBXHCI!UsbDevice_UcxEvtEndpointsConfigure
    EvtUsbDeviceEnable: (0xfffff880044cffac) USBXHCI!UsbDevice_UcxEvtEnable
    EvtUsbDeviceDisable: (0xfffff880044d1cbc) USBXHCI!UsbDevice_UcxEvtDisable
    EvtUsbDeviceReset: (0xfffff880044d2178) USBXHCI!UsbDevice_UcxEvtReset
    EvtUsbDeviceAddress: (0xfffff880044d0934) USBXHCI!UsbDevice_UcxEvtAddress
    EvtUsbDeviceUpdate: (0xfffff880044d0c80) USBXHCI!UsbDevice_UcxEvtUpdate
    EvtUsbDeviceDefaultEndpointAdd: (0xfffff880044ede1c) USBXHCI!Endpoint_UcxEvtUsbDeviceDefaultEndpointAdd
    EvtUsbDeviceEndpointAdd: (0xfffff880044edfc8) USBXHCI!Endpoint_UcxEvtUsbDeviceEndpointAdd
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[USB 3.0 の拡張機能](usb-3-extensions.md)

[**! usb3kd.ucx\_コント ローラー\_一覧**](-usb3kd-ucx-controller-list.md)

[ユニバーサル シリアル バス (USB) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






