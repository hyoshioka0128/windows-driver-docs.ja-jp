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
ms.openlocfilehash: 94981e59cd11e152cd201aaab1b4032290fac0f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348236"
---
# <a name="guidclassusbdevice"></a>GUID_CLASS_USB_DEVICE


GUID_CLASS_USB_DEVICE は古い形式の識別子、[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)の[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930) USB ハブに接続されているデバイス。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_USB_DEVICE** ](guid-devinterface-usb-device.md)このクラスの新しいインスタンスのクラス識別子。

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

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

 

 






