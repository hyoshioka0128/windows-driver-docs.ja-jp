---
title: EFI_USBFN_DEVICE_INFO_ID
description: EFI_USBFN_DEVICE_INFO_ID
ms.assetid: bc0391b4-876a-4c3c-920c-a16a781a84b0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bbe90b7630b391c8c7a32d76b06518fc23dab10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581826"
---
# <a name="efiusbfndeviceinfoid"></a>EFI\_USBFN\_デバイス\_情報\_ID


この列挙は、ドライバーへの要求で特定の文字列を識別するために使用されます。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_USBFN_DEVICE_INFO_ID   
{
    EfiUsbDeviceInfoUnknown = 0,
    EfiUsbDeviceInfoSerialNumber,
    EfiUsbDeviceInfoManufacturerName,
    EfiUsbDeviceInfoProductName
} EFI_USBFN_DEVICE_INFO_ID;
```

## <a name="constants"></a>定数


<a href="" id="efiusbdeviceinfounknown"></a>**EfiUsbDeviceInfoUnknown**  
無効な id。

<a href="" id="efiusbdeviceinfoserialnumber"></a>**EfiUsbDeviceInfoSerialNumber**  
USB デバイスのシリアル番号を要求します。

<a href="" id="efiusbdeviceinfomanufacturername"></a>**EfiUsbDeviceInfoManufacturerName**  
製造元の文字列を要求します。

<a href="" id="efiusbdeviceinfoproductname"></a>**EfiUsbDeviceInfoProductName**  
デバイスの製品名の要求。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




