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
ms.openlocfilehash: a00e2e14182c917beaae3a76185177ae6752ea94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391998"
---
# <a name="guiddevinterfaceusbdevice"></a>GUID_DEVINTERFACE_USB_DEVICE


GUID_DEVINTERFACE_USB_DEVICE[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている[USB デバイス](https://msdn.microsoft.com/library/windows/hardware/ff538930)USB ハブに接続されています。

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

<a name="requirements"></a>要件
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

 

 






