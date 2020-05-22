---
title: EFI_USB_DEVICE_INFO
description: EFI_USB_DEVICE_INFO
ms.assetid: b44f77fc-f496-488f-b53a-b54420da9360
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: c7c46a0c50fd44ace90f77041681a9ca95437f7b
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778340"
---
# <a name="efi_usb_device_info"></a>EFI \_ USB \_ デバイス \_ 情報

**EFI \_ usb \_ デバイス \_ 情報**構造は、usb 機能デバイスを定義するために使用されます。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    EFI_USB_DEVICE_DESCRIPTOR           *DeviceDescriptor;
    EFI_USB_CONFIG_INFO                 **ConfigInfoTable;
} EFI_USB_DEVICE_INFO;
```

## <a name="members"></a>メンバー

### <a name="devicedescriptor"></a>DeviceDescriptor

\_ \_ \_ Usb デバイスの構成情報が格納されている EFI usb デバイス記述子構造体。

### <a name="configinfotable"></a>ConfigInfoTable

サポートされている \_ \_ \_ 構成に関する情報が含まれている EFI USB 構成情報の構造。

## <a name="remarks"></a>解説

**Efi \_ usb \_ 構成 \_ 記述子**と**efi \_ USB \_ デバイス \_ 記述子**の構造は、UEFI 仕様2.3 で定義されています。 詳細については、 [UEFI.org](https://uefi.org/specifications)の web サイトを参照してください。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
