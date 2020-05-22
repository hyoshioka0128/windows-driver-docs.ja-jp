---
title: EFI_USB_SUPERSPEED_INTERFACE_INFO
description: EFI_USB_SUPERSPEED_INTERFACE_INFO
ms.assetid: 1B0C04D0-5254-4B9A-A94D-4FF1CEAD4627
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5b25187ba0193cd30e58316f6caa7780faa6f83e
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778324"
---
# <a name="efi_usb_superspeed_interface_info"></a>EFI \_ USB \_ SUPERSPEED \_ インターフェイス \_ 情報

**EFI \_ usb \_ SUPERSPEED \_ interface \_ INFO**構造体は、usb 関数ドライバーに対してサポートされている usb SUPERSPEED インターフェイスを定義するために使用されます。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    EFI_USB_INTERFACE_DESCRIPTOR            *InterfaceDescriptor;
    EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR  **EndpointDescriptorTable;
} EFI_USB_SUPERSPEED_INTERFACE_INFO;
```

## <a name="members"></a>メンバー

### <a name="interfacedescriptor"></a>InterfaceDescriptor

\_ \_ \_ Usb 関数インターフェイスを記述する EFI usb インターフェイス記述子の構造体。

### <a name="endpointdescriptortable"></a>Endpoint記述子テーブル

USB SuperSpeed エンドポイントを記述する[EFI \_ usb \_ SUPERSPEED \_ エンドポイント \_ 記述子](efi-usb-superspeed-endpoint-descriptor.md)構造体。

## <a name="remarks"></a>解説

**EFI \_ USB \_ インターフェイス \_ 記述子**の構造は、UEFI 仕様バージョン2.3 以降で定義されています。 詳細については、 [UEFI.org](https://uefi.org/specifications)の web サイトを参照してください。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
