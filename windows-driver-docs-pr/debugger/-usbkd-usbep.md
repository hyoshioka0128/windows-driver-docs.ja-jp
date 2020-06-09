---
title: usbkd. usbep
description: Usbkd. usbep コマンドは、USB エンドポイントに関する情報を表示します。
ms.assetid: FEF66394-0502-4F3F-ACBE-57AA1945CC74
keywords:
- usbkd. usbep Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbep
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1227cf98b6c0ba4b3e664077ca1ac4d3e84eb994
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534701"
---
# <a name="usbkdusbep"></a>!usbkd.usbep


**! Usbkd. usbep**コマンドは、USB エンドポイントに関する情報を表示します。

```dbgcmd
!usbkd.usbep StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
**Usbport のアドレス。 \_HCD \_ エンドポイント**構造体。 USB ホストコントローラーのエンドポイント一覧を取得するには、 [**usbhcdext**](-usbkd-usbhcdext.md)コマンドを使用します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd .dll

<a name="examples"></a>例
--------

Usbport のアドレスを確認する方法の1つを次に示し**ます。 \_HCD \_ エンドポイント**構造体。 最初に「 [**! usbkd**](-usbkd-usb2tree.md)」と入力します。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

上記の出力では、FDO のデバイス拡張機能のアドレスが、 [DML](debugger-markup-language-commands.md)コマンドの引数として表示されます **! ehci \_ info ffffe00001ca11a0**です。

[DML] コマンドをクリックするか、デバイス拡張機能のアドレスを[**! usbhcdext**](-usbkd-usbhcdext.md)に渡して、グローバルエンドポイントリストを取得します。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0
...
DeviceHandleList: !usblist ffffe00001ca23b8, DL 
DeviceHandleDeletedList: !usblist ffffe00001ca23c8, DL [Empty]
GlobalEndpointList: !usblist ffffe00001ca2388, EP 
...
```

次に、 [**! usbkd**](-usbkd-usblist.md)コマンドを使用して、 ** \_ \_ エンドポイント**構造体のアドレスを取得します。

```dbgcmd
0: kd> !usblist ffffe00001ca2388, EP

list: ffffe00001ca2388 EP
----------
dt usbport!_HCD_ENDPOINT ffffe000020f6970  !usbep ffffe000020f6970
Device Address: 0x00, ep 0x00 Control  Flags: 00000002 dt _USB_ENDPOINT_FLAGS ffffe000020f6990
dt usbport!_ENDPOINT_PARAMETERS ffffe000020f6b18    RootHub Endpoint
...
```

前の出力で、 `ffffe000020f6970 ` は** \_ HCD \_ エンドポイント**構造体のアドレスです。 このアドレスを **! usbkd. usbep**に渡します。

```dbgcmd
0: kd> !usbep ffffe000020f6970
Device Address: 0x00, Endpoint Address 0x00 Endpoint Type: Control 
dt USBPORT!_HCD_ENDPOINT ffffe000020f6970
dt USBPORT!_ENDPOINT_PARAMETERS ffffe000020f6b18
RootHub Endpoint

## Transfer(s) List: (HwPendingListHead)

    [EMPTY]

## Endpoint Reference List: (EpRefListHead)

[00] dt USBPORT!_USBOBJ_REF ffffe000021a64a0 Object ffffe000020f6970 Tag:EPop Endpoint:ffffe000020f6970
[01] dt USBPORT!_USBOBJ_REF ffffe000021264a0 Object ffffe000020f95e0 Tag:EPpi Endpoint:ffffe000020f6970

## GEP HISTORY (latest at bottom)

##      EVENT                   STATE                     NEXT                      HwEpState

[01] Ev_gEp_Open             GEp_Init                  GEp_Paused                ENDPOINT_PAUSE
[02] Ev_gEp_ReqActive        GEp_Paused                GEp_Active                ENDPOINT_ACTIVE
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[USB 2.0 デバッガー拡張機能](usb-2-0-extensions.md)

[ユニバーサルシリアルバス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






