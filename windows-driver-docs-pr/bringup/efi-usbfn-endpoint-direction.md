---
title: EFI_USBFN_ENDPOINT_DIRECTION
description: EFI_USBFN_ENDPOINT_DIRECTION
ms.assetid: 910f7ab5-b4c0-4385-9306-37d863d19bf7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f45aef9754542f8242294e1fcb2229478cd0d05c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580417"
---
# <a name="efiusbfnendpointdirection"></a>EFI\_USBFN\_エンドポイント\_方向


**EFI\_USBFN\_エンドポイント\_方向**列挙体は、USB 転送の方向を識別するために使用します。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_USBFN_ENDPOINT_DIRECTION 
{
    EfiUsbEndpointDirectionHostOut  = 0,
    EfiUsbEndpointDirectionHostIn,
    EfiUsbEndpointDirectionDeviceTx = EfiUsbEndpointDirectionHostIn,
    EfiUsbEndpointDirectionDeviceRx = EfiUsbEndpointDirectionHostOut
} EFI_USBFN_ENDPOINT_DIRECTION;
```

## <a name="constants"></a>定数


<a href="" id="efiusbendpointdirectionhostout"></a>**EfiUsbEndpointDirectionHostOut**  
USB を転送を示します。 D irection がホストからデバイスには

<a href="" id="efiusbendpointdirectionhostin"></a>**EfiUsbEndpointDirectionHostIn**  
USB の転送を示します。 方向は、デバイスからホストです。

<a href="" id="efiusbendpointdirectiondevicetx"></a>**EfiUsbEndpointDirectionDeviceTx**  
USB の転送を示します。 方向は、デバイスからホストです。

<a href="" id="efiusbendpointdirectiondevicerx"></a>**EfiUsbEndpointDirectionDeviceRx**  
USB を転送を示します。 方向は、ホストからデバイスには

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




