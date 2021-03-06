---
title: GUID_DEVINTERFACE_USB_HUB
description: GUID_DEVINTERFACE_USB_HUB
ms.assetid: 899b77ad-fa98-4078-9207-69b422e3d0d0
keywords:
- GUID_DEVINTERFACE_USB_HUB デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_USB_HUB
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c275175f089390d8a7eda8dda1c7d16347c59e6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386418"
---
# <a name="guiddevinterfaceusbhub"></a>GUID_DEVINTERFACE_USB_HUB


GUID_DEVINTERFACE_USB_HUB[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている[USB](https://docs.microsoft.com/windows-hardware/drivers/)ハブのデバイス。

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
<td align="left"><p>GUID_DEVINTERFACE_USB_HUB</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{F18A0E88-C30C-11D0-8815-00A0C906BED8}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム提供の USB ポート ドライバーでは、オペレーティング システムとアプリケーションのホスト コント ローラー デバイスのルート ハブの存在を通知する GUID_DEVINTERFACE_USB_HUB のインスタンスを登録します。 USB ハブのシステムによって提供されるドライバーは、あるホスト コント ローラーでサポートされている場合、追加ハブ デバイスの場合は、このクラスのインスタンスを登録します。

Microsoft Windows Driver Kit (WDK) が含まれています、 [USBVIEW サンプル アプリケーション](https://go.microsoft.com/fwlink/p/?linkid=256205)します。 USBVIEW サンプルが古い形式の識別子を使用して[ **GUID_CLASS_USBHUB** ](guid-class-usbhub.md)このデバイスのインターフェイス クラスのインスタンスの通知を受け取る。

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


[**GUID_CLASS_USBHUB**](guid-class-usbhub.md)

[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

[**GUID_DEVINTERFACE_USB_HOST_CONTROLLER**](guid-devinterface-usb-host-controller.md)

 

 






