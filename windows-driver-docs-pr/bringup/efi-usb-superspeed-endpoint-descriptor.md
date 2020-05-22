---
title: EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR
description: EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR
ms.assetid: 3254C0F1-85C2-472B-938A-F71645703540
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: cb9670a81c73ab3f33b0308a1a54a95daf495d94
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778336"
---
# <a name="efi_usb_superspeed_endpoint_descriptor"></a>EFI \_ USB \_ SUPERSPEED \_ エンドポイント \_ 記述子

**EFI \_ usb \_ SUPERSPEED \_ エンドポイント \_ 記述子**構造は、usb 関数ドライバーに対してサポートされている usb SUPERSPEED エンドポイントを説明するために使用されます。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    EFI_USB_ENDPOINT_DESCRIPTOR                         *EndpointDescriptor;
    EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR    *EndpointCompanionDescriptor;
} EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR;
```

## <a name="members"></a>メンバー

### <a name="endpointdescriptor"></a>EndpointDescriptor

\_ \_ Usb エンドポイントを記述する EFI usb エンドポイント \_ 記述子の構造体。

### <a name="endpointcompaniondescriptor"></a>EndpointCompanionDescriptor

USB SuperSpeed エンドポイントのコンパニオン記述子である[EFI \_ USB \_ SUPERSPEED \_ エンドポイント \_ コンパニオン \_ 記述子](efi-usb-superspeed-endpoint-companion-descriptor.md)構造体。

## <a name="remarks"></a>解説

**EFI \_ USB \_ エンドポイント \_ 記述子**の構造は、UEFI 仕様バージョン2.3 以降で定義されています。 詳細については、 [UEFI.org](https://uefi.org/specifications)の web サイトを参照してください。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
