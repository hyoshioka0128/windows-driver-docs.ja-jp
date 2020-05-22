---
title: EFI_USB_CONFIG_INFO
description: EFI_USB_CONFIG_INFO
ms.assetid: 74d5cb02-2648-4bd1-990e-61156b5dc8cd
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 10ae4734244bc6fa4f5f1ae6d0cdb8511a5788c6
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778332"
---
# <a name="efi_usb_config_info"></a>EFI \_ USB \_ 構成 \_ 情報

**EFI \_ usb \_ 構成 \_ 情報**の構造を使用して、サポートされている usb ポート構成を定義します。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_INTERFACE_INFO              **InterfaceInfoTable;
} EFI_USB_CONFIG_INFO;
```

## <a name="members"></a>メンバー

### <a name="configdescriptor"></a>ConfigDescriptor

\_ \_ \_ Usb 機能デバイスの構成情報を含む EFI usb 構成記述子の構造体。

### <a name="interfaceinfotable"></a>InterfaceInfoTable

サポートされているインターフェイスに関する情報を含む[EFI \_ USB \_ インターフェイス \_ 情報](efi-usb-interface-info.md)構造体。

## <a name="remarks"></a>解説

構造体の**USB \_ 構成 \_ 記述子**は、UEFI 仕様2.3 で定義されています。 詳細については、 [UEFI.org](https://uefi.org/specifications)の web サイトを参照してください。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
