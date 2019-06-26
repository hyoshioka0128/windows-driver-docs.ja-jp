---
title: GUID_CLASS_USB_DEVICE
description: GUID_CLASS_USB_DEVICE
ms.assetid: e014f3d5-541d-4e86-a572-b110ec5a822d
keywords:
- GUID_CLASS_USB_DEVICE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_CLASS_USB_DEVICE
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 36daa743555be8308383603ac7f773a0ec96c624
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355505"
---
# <a name="guidclassusbdevice"></a>GUID_CLASS_USB_DEVICE


GUID_CLASS_USB_DEVICE は古い形式の識別子、[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)の[USB](https://docs.microsoft.com/windows-hardware/drivers/) USB ハブに接続されているデバイス。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_USB_DEVICE** ](guid-devinterface-usb-device.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>注釈
-------

Microsoft Windows Driver Kit (WDK) が含まれています、 [USBVIEW サンプル アプリケーション](https://go.microsoft.com/fwlink/p/?linkid=256205)します。 USBVIEW サンプルでは、GUID_CLASS_USB_DEVICE を使用して、GUID_CLASS_USB_DEVICE インターフェイス クラスのインスタンスが存在する場合は通知に登録します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>使われていません。 Windows 2000 以降、GUID_DEVINTERFACE_USB_DEVICE を代わりに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Usbiodef.h (Usbiodef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>注釈

以前は、この識別子に依存した`Usbioctl.h`します。  今すぐに含める必要がありますので注意`Usbiodef.h`代わりにします。

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

 

 






