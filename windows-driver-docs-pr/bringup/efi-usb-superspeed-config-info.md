---
title: EFI_USB_SUPERSPEED_CONFIG_INFO
description: EFI_USB_SUPERSPEED_CONFIG_INFO
ms.assetid: 9827B0A9-AC69-43FA-922F-384E3AE140F7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f336370023fff9ddd185c6c4f2b56140499240a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337749"
---
# <a name="efiusbsuperspeedconfiginfo"></a>EFI\_USB\_SUPERSPEED\_CONFIG\_情報


**EFI\_USB\_SUPERSPEED\_CONFIG\_情報**USB 機能ドライバーをサポートされている USB SuperSpeed ポートの構成を定義する構造を使用します。

## <a name="syntax"></a>構文


```cpp
typedef struct
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_SUPERSPEED_INTERFACE_INFO   **InterfaceInfoTable;
} EFI_USB_SUPERSPEED_CONFIG_INFO;
```

## <a name="members"></a>メンバー


<a href="" id="configdescriptor"></a>**ConfigDescriptor**  
EFI\_USB\_CONFIG\_関数の USB デバイスの構成記述子を含む記述子構造体。

<a href="" id="interfaceinfotable"></a>**InterfaceInfoTable**  
[EFI\_USB\_SUPERSPEED\_インターフェイス\_情報](efi-usb-superspeed-interface-info.md)サポートされている USB SuperSpeed インターフェイスを記述する構造体。

## <a name="remarks"></a>注釈


**EFI\_USB\_CONFIG\_記述子**構造体は、UEFI 仕様バージョン 2.3 で定義されている以降。 詳細については、次を参照してください。、 [UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526) web サイト。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




