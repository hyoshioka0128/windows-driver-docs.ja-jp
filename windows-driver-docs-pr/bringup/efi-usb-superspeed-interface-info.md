---
title: EFI_USB_SUPERSPEED_INTERFACE_INFO
description: EFI_USB_SUPERSPEED_INTERFACE_INFO
ms.assetid: 1B0C04D0-5254-4B9A-A94D-4FF1CEAD4627
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7e4b98501f0e99df7bec364d6ff1a91ff2d47d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573016"
---
# <a name="efiusbsuperspeedinterfaceinfo"></a>EFI\_USB\_SUPERSPEED\_インターフェイス\_情報


**EFI\_USB\_SUPERSPEED\_インターフェイス\_情報**構造体がインターフェイスを定義する、サポートされている USB SuperSpeed USB 機能ドライバーを使用します。

## <a name="syntax"></a>構文


```cpp
typedef struct
{
    EFI_USB_INTERFACE_DESCRIPTOR            *InterfaceDescriptor;
    EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR  **EndpointDescriptorTable; 
} EFI_USB_SUPERSPEED_INTERFACE_INFO;
```

## <a name="members"></a>メンバー


<a href="" id="interfacedescriptor"></a>**InterfaceDescriptor**  
EFI\_USB\_インターフェイス\_USB 関数のインターフェイスを記述する記述子構造体。

<a href="" id="endpointdescriptortable"></a>**EndpointDescriptorTable**  
[EFI\_USB\_SUPERSPEED\_エンドポイント\_記述子](efi-usb-superspeed-endpoint-descriptor.md)USB SuperSpeed エンドポイントを記述する構造体。

## <a name="remarks"></a>コメント


**EFI\_USB\_インターフェイス\_記述子**構造体は、UEFI 仕様バージョン 2.3 で定義されている以降。 詳細については、次を参照してください。、 [UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526) web サイト。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




