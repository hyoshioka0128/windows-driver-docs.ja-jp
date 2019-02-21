---
title: EFI_USBFN_MESSAGE_PAYLOAD
description: EFI_USBFN_MESSAGE_PAYLOAD
ms.assetid: 88d32ce1-460d-4c0f-b42a-426f42e2f969
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00b32ff2827250cde4e627c71982a5eb3fdae81d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539464"
---
# <a name="efiusbfnmessagepayload"></a>EFI\_USBFN\_メッセージ\_ペイロード


**EFI\_USBFN\_メッセージ\_ペイロード**共用体には、現在のメッセージの追加のペイロード (デバイスの要求、転送の結果またはバス速度の情報) が含まれています。

## <a name="syntax"></a>構文


```cpp
typedef union _EFI_USBFN_MESSAGE_PAYLOAD
{
    EFI_USB_DEVICE_REQUEST      udr;
    EFI_USBFN_TRANSFER_RESULT   utr;
    EFI_USB_BUS_SPEED           ubs;
} EFI_USBFN_MESSAGE_PAYLOAD;
```

## <a name="members"></a>Members


<a href="" id="udr"></a>**udr**  
A **EFI\_USB\_デバイス\_要求**デバイス要求に関する情報を含む構造体。

<a href="" id="utr"></a>**utr**  
A [EFI\_USBFN\_転送\_結果](efi-usbfn-transfer-result.md)転送結果に関する情報を含む構造体。

<a href="" id="ubs"></a>**ubs**  
A [EFI\_USB\_BUS\_速度](efi-usb-bus-speed.md)バス速度の USB を示す列挙値。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




