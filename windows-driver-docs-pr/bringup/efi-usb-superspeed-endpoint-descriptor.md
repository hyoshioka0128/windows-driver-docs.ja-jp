---
title: EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR
description: EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR
ms.assetid: 3254C0F1-85C2-472B-938A-F71645703540
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 707369e918301a1b1f3387e6253a8235b078a119
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580558"
---
# <a name="efiusbsuperspeedendpointdescriptor"></a>EFI\_USB\_SUPERSPEED\_エンドポイント\_記述子


**EFI\_USB\_SUPERSPEED\_エンドポイント\_記述子**構造を使用して USB 機能ドライバーをサポートされている USB SuperSpeed エンドポイントについて説明します。

## <a name="syntax"></a>構文


```cpp
typedef struct
{
    EFI_USB_ENDPOINT_DESCRIPTOR                         *EndpointDescriptor;
    EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR    *EndpointCompanionDescriptor;
} EFI_USB_SUPERSPEED_ENDPOINT_DESCRIPTOR;
```

## <a name="members"></a>メンバー


<a href="" id="endpointdescriptor"></a>**EndpointDescriptor**  
EFI\_USB\_エンドポイント\_USB エンドポイントを記述する記述子構造体。

<a href="" id="endpointcompaniondescriptor"></a>**EndpointCompanionDescriptor**  
[EFI\_USB\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子](efi-usb-superspeed-endpoint-companion-descriptor.md)USB SuperSpeed エンドポイント コンパニオンの記述子構造体。

## <a name="remarks"></a>コメント


**EFI\_USB\_エンドポイント\_記述子**構造体は、UEFI 仕様バージョン 2.3 で定義されている以降。 詳細については、次を参照してください。、 [UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526) web サイト。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




