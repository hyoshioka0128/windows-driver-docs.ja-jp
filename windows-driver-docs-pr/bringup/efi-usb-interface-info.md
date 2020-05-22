---
title: EFI_USB_INTERFACE_INFO
description: EFI_USB_INTERFACE_INFO
ms.assetid: d20b78bd-8369-4f50-b161-e8ad0bb4c52f
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8c1381d2350fe162607816011e5b4fa9393783c3
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778334"
---
# <a name="efi_usb_interface_info"></a>EFI \_ USB \_ インターフェイス \_ 情報

サポートされている USB インターフェイスを定義するために使用される**EFI \_ USB \_ インターフェイス \_ 情報**構造。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    EFI_USB_INTERFACE_DESCRIPTOR        *InterfaceDescriptor;
    EFI_USB_ENDPOINT_DESCRIPTOR         **EndpointDescriptorTable;
} EFI_USB_INTERFACE_INFO;
```

## <a name="members"></a>メンバー

### <a name="interfacedescriptor"></a>InterfaceDescriptor

\_ \_ \_ Usb 関数インターフェイスに関する情報を含む EFI usb インターフェイス記述子の構造体。

### <a name="endpointdescriptortable"></a>Endpoint記述子テーブル

\_ \_ サポートされて \_ いるエンドポイントに関する情報を格納している EFI USB エンドポイント記述子の構造体。

## <a name="remarks"></a>解説

**Usb \_ インターフェイス \_ 記述子**と**usb \_ エンドポイント \_ 記述子**の構造は、UEFI 仕様2.3 で定義されています。 詳細については、 [UEFI.org](https://uefi.org/specifications)の web サイトを参照してください。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
