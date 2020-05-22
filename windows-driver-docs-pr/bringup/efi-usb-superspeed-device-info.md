---
title: EFI_USB_SUPERSPEED_DEVICE_INFO
description: EFI_USB_SUPERSPEED_DEVICE_INFO
ms.assetid: 7861BA16-7499-48A1-9D6A-9BB8F5AA36CE
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: a059ff06fc2359c2a9ae62a0e3d25fae6476039f
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778328"
---
# <a name="efi_usb_superspeed_device_info"></a>EFI \_ USB \_ SUPERSPEED \_ デバイス \_ 情報

**EFI \_ usb \_ SUPERSPEED \_ device \_ INFO**構造体は、usb SUPERSPEED 関数デバイスを定義するために使用されます。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    EFI_USB_DEVICE_DESCRIPTOR           *DeviceDescriptor;
    EFI_USB_SUPERSPEED_CONFIG_INFO      **ConfigInfoTable;
    EFI_USB_BOS_DESCRIPTOR              *BosDescriptor
} EFI_USB_SUPERSPEED_DEVICE_INFO;
```

## <a name="members"></a>メンバー

### <a name="devicedescriptor"></a>DeviceDescriptor

\_ \_ \_ Usb デバイスの構成情報が格納されている EFI usb デバイス記述子構造体。

### <a name="configinfotable"></a>ConfigInfoTable

サポートされている USB SuperSpeed 構成に関する情報が含まれている[EFI \_ USB \_ SUPERSPEED \_ CONFIG \_ INFO](efi-usb-superspeed-config-info.md)構造体。

### <a name="bosdescriptor"></a>BosDescriptor

USB 関数ドライバーへのバイナリオブジェクトストアに関する情報を含む[EFI \_ USB \_ BOS \_ 記述子](efi-usb-bos-descriptor.md)構造体。

## <a name="remarks"></a>解説

**EFI \_ USB \_ 構成 \_ 記述子**の構造は、UEFI 仕様バージョン2.3 以降で定義されています。 詳細については、 [UEFI.org](https://uefi.org/specifications)の web サイトを参照してください。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
