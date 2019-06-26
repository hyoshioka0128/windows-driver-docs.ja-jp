---
title: GUID_DEVINTERFACE_USB_DEVICE
description: GUID_DEVINTERFACE_USB_DEVICE
ms.assetid: 9a771eca-8ec5-4c69-8b1e-f01f548b5041
keywords:
- GUID_DEVINTERFACE_USB_DEVICE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_USB_DEVICE
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f7d2d1c7a27d3e021db02bbb495a05874efd58a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353789"
---
# <a name="guiddevinterfaceusbdevice"></a>GUID_DEVINTERFACE_USB_DEVICE


GUID_DEVINTERFACE_USB_DEVICE[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている[USB デバイス](https://docs.microsoft.com/windows-hardware/drivers/)USB ハブに接続されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>GUID_DEVINTERFACE_USB_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{A5DCBF10-6530-11D2-901F-00C04FB951ED}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム提供の USB ハブのドライバーでは、システムと USB ハブに接続されている USB デバイスの存在をアプリケーションに通知する GUID_DEVINTERFACE_USB_DEVICE のインスタンスを登録します。

Microsoft Windows Driver Kit (WDK) が含まれています、 [USBVIEW サンプル アプリケーション](https://go.microsoft.com/fwlink/p/?linkid=256205)します。 USBVIEW サンプルが古い形式の識別子を使用して[ **GUID_CLASS_USB_DEVICE** ](guid-class-usb-device.md)このデバイスのインターフェイス クラスのインスタンスの到着を通知に登録します。

Initguid.h は DEFINE_GUID マクロを使用して GUID を宣言するすべてのヘッダーをインクルードする前に含める必要があります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Usbiodef.h (Usbiodef.h、含める initguid.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_CLASS_USB_DEVICE**](guid-class-usb-device.md)

[**GUID_DEVINTERFACE_USB_HOST_CONTROLLER**](guid-devinterface-usb-host-controller.md)

[**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md)

 

 






