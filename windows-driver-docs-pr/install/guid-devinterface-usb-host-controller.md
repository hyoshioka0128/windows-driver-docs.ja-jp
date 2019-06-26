---
title: GUID_DEVINTERFACE_USB_HOST_CONTROLLER
description: GUID_DEVINTERFACE_USB_HOST_CONTROLLER
ms.assetid: 4afa1ada-ff57-4585-9117-10595310b976
keywords:
- GUID_DEVINTERFACE_USB_HOST_CONTROLLER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_USB_HOST_CONTROLLER
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ed4ac5d10ebfe13172c9b482020ec78e7a4da1ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386424"
---
# <a name="guiddevinterfaceusbhostcontroller"></a>GUID_DEVINTERFACE_USB_HOST_CONTROLLER


GUID_DEVINTERFACE_USB_HOST_CONTROLLER[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている[USB](https://docs.microsoft.com/windows-hardware/drivers/)コント ローラー デバイスをホストします。

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
<td align="left"><p>GUID_DEVINTERFACE_USB_HOST_CONTROLLER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{3ABF6F2D-71C4-462A-8A92-1E6861E6AF27}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム指定のポートのドライバーを USB ホスト コント ローラーは、オペレーティング システムと USB ホスト コント ローラーの存在をアプリケーションに通知する GUID_DEVINTERFACE_USB_HOST_CONTROLLER のインスタンスを登録します。

Microsoft Windows Driver Kit (WDK) が含まれています、 [USBVIEW サンプル アプリケーション](https://go.microsoft.com/fwlink/p/?linkid=256205)します。 USBVIEW が古い形式の識別子を使用して[ **GUID_CLASS_USB_HOST_CONTROLLER** ](guid-class-usb-host-controller.md)このデバイスのインターフェイス クラスのインスタンスを列挙します。

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


[**GUID_CLASS_USB_HOST_CONTROLLER**](guid-class-usb-host-controller.md)

[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

[**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md)

 

 






