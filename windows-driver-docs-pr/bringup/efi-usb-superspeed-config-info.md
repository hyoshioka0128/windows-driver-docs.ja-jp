---
title: EFI_USB_SUPERSPEED_CONFIG_INFO
description: EFI_USB_SUPERSPEED_CONFIG_INFO
ms.assetid: 9827B0A9-AC69-43FA-922F-384E3AE140F7
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 82dd63ae4989f03550f11d4d1a37aff86db994df
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778326"
---
# <a name="efi_usb_superspeed_config_info"></a>EFI \_ USB \_ SUPERSPEED \_ 構成 \_ 情報

**EFI \_ usb \_ SUPERSPEED \_ CONFIG \_ INFO**構造体は、usb 関数ドライバーに対してサポートされている usb SUPERSPEED ポート構成を定義するために使用されます。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_SUPERSPEED_INTERFACE_INFO   **InterfaceInfoTable;
} EFI_USB_SUPERSPEED_CONFIG_INFO;
```

## <a name="members"></a>メンバー

### <a name="configdescriptor"></a>ConfigDescriptor

\_ \_ \_ Usb 機能デバイスの構成記述子を含む EFI USB 構成記述子の構造体。

### <a name="interfaceinfotable"></a>InterfaceInfoTable

サポートされている USB SuperSpeed インターフェイスを記述する[EFI \_ USB \_ SUPERSPEED \_ INTERFACE \_ INFO](efi-usb-superspeed-interface-info.md)構造体。

## <a name="remarks"></a>解説

**EFI \_ USB \_ 構成 \_ 記述子**の構造は、UEFI 仕様バージョン2.3 以降で定義されています。 詳細については、 [UEFI.org](https://uefi.org/specifications)の web サイトを参照してください。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
