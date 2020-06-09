---
title: ucx_device usb3kd
description: Ucx_device usb3kd 拡張機能は、usb デバイスに関する情報を USB 3.0 ツリーに表示します。 表示は、UcxVersion. sys によって管理されるデータ構造に基づいています。
ms.assetid: 7AC3DBBF-1D62-492E-B46E-C193579DE1E3
keywords:
- usb3kd Windows デバッグの ucx_device
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_device
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 019e52da6acb3d0e5fa9702d93593d2e72c91cb7
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534155"
---
# <a name="usb3kducx_device"></a>! usb3kd \_ デバイス


[**! Usb3kd \_ デバイス**](-usb3kd-device-info.md)拡張機能では、usb デバイスに関する情報が[usb 3.0 ツリー](usb-3-extensions.md#usb-3-tree)に表示されます。 この表示は、USB ホストコントローラー拡張機能ドライバー (Ucx*バージョン*.sys) によって管理されるデータ構造に基づいています。

```dbgcmd
!usb3kd.ucx_device UcxUsbDevicePrivContext
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______UcxUsbDevicePrivContext______"></span><span id="_______ucxusbdeviceprivcontext______"></span><span id="_______UCXUSBDEVICEPRIVCONTEXT______"></span>*Ucxusbdeviceprivcontext*   
\_デバイスを表す ucxusbdevice \_ privcontext 構造体のアドレス。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd

<a name="remarks"></a>注釈
-------

Usb ホストコントローラー拡張機能ドライバー (Ucx*バージョン*.sys) は、usb 3.0 ハブドライバーと usb 3.0 ホストコントローラードライバーの間に抽象層を提供します。 拡張機能ドライバーは、ホストコントローラー、デバイス、およびエンドポイントを独自に表現したものです。 出力[**! ucx \_ デバイス**](-usb3kd-device-info.md)コマンドは、拡張機能ドライバーによって保持されているデータ構造に基づいています。 Usb ホストコントローラー拡張機能ドライバーおよび USB 3.0 ホストコントローラードライバーの詳細については、「 [Usb ドライバースタックアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

**! ucx \_ デバイス**と[**! デバイス \_ 情報**](-usb3kd-device-info.md)はどちらもデバイスに関する情報を表示しますが、表示される情報は異なります。 **! Ucx \_ デバイス**の出力は、usb ホストコントローラー拡張機能ドライバーの観点から見ると、**デバイス \_ 情報**の出力は、usb 3.0 hub ドライバーの観点からのものです。 たとえば、 **! ucx \_ デバイス**出力には、エンドポイントに関する情報が含まれています。また、 **! デバイス \_ 情報**出力には、構成およびインターフェイス記述子に関する情報が含まれています。

<a name="examples"></a>例
--------

UCX USB デバイスのプライベートコンテキストのアドレスを取得するには、 [**! ucx \_ controller \_ list**](-usb3kd-ucx-controller-list.md)コマンドの出力を確認します。 次の例では、2番目のデバイスのプライベートコンテキストのアドレスは0xfffffa8005bd9680 です。

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

これで、UCX USB プライベートコンテキストのアドレスを **! ucx \_ デバイス**コマンドに渡すことができるようになりました。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 3.0 拡張機能](usb-3-extensions.md)

[**! usb3kd \_ コントローラーの \_ 一覧**](-usb3kd-ucx-controller-list.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






