---
title: EFI_USB_BUS_SPEED
description: EFI_USB_BUS_SPEED
ms.assetid: 2888cff6-db12-47ea-866f-de218e2b08e5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 179b6a0befdecc81e05d2fae07352396251f1d3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337795"
---
# <a name="efiusbbusspeed"></a>EFI\_USB\_BUS\_速度


列挙には、バス速度を示すために使用される値が含まれています。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_USB_BUS_SPEED 
{
    UsbBusSpeedUnknown = 0,
    UsbBusSpeedLow,
    UsbBusSpeedFull,
    UsbBusSpeedHigh,
    UsbBusSpeedSuper,
    UsbBusSpeedMaximum = UsbBusSpeedSuper
} EFI_USB_BUS_SPEED;
```

## <a name="constants"></a>定数


<a href="" id="usbbusspeedunknown"></a>**UsbBusSpeedUnknown**  
バス速度が不明です。

<a href="" id="usbbusspeedlow"></a>**UsbBusSpeedLow**  
低速です。

<a href="" id="usbbusspeedfull"></a>**UsbBusSpeedFull**  
完全な速度です。

<a href="" id="usbbusspeedhigh"></a>**UsbBusSpeedHigh**  
高速です。

<a href="" id="usbbusspeedsuper"></a>**UsbBusSpeedSuper**  
超高速です。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




