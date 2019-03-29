---
title: EFI_USB_ENDPOINT_TYPE
description: EFI_USB_ENDPOINT_TYPE
ms.assetid: 5cdb0efc-2355-42e2-929b-df19257e35c1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2b3a6ea6199962da8716c62d271676f999aa3b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573017"
---
# <a name="efiusbendpointtype"></a>EFI\_USB\_エンドポイント\_型


**EFI\_USB\_エンドポイント\_型**列挙には、エンドポイントの種類を示すために使用される値が含まれています。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_USB_ENDPOINT_TYPE{
  UsbEndpointControl = 0x00,
  UsbEndpointIsochronous = 0x01,
  UsbEndpointBulk = 0x02,
  UsbEndpointInterrupt = 0x03
} EFI_USB_ENDPOINT_TYPE;
```

## <a name="constants"></a>定数


<a href="" id="usbendpointcontrol"></a>**UsbEndpointControl**  
転送の制御コマンドと状態の操作。

<a href="" id="usbendpointisochronous"></a>**UsbEndpointIsochronous**  
アイソクロナス transfe - 保証された帯域幅と待機時間の境界のある機密データを時間の連続するストリーム。

<a href="" id="usbendpointbulk"></a>**UsbEndpointBulk**  
一括転送 - 大量データの急激な増加の帯域幅、または最小の待機時間の保証はありません。

<a href="" id="usbendpointinterrupt"></a>**UsbEndpointInterrupt**  
転送 - 非定期的な通信の最大待機時間の保証を中断します。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




