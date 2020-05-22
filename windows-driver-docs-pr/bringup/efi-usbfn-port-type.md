---
title: EFI_USBFN_PORT_TYPE
description: EFI_USBFN_PORT_TYPE
ms.assetid: 2596dd4f-26bd-454b-9550-a89c7e1f790b
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: c1cf7fe654a7fdfef36ba8c0b00f3eee0caba7b9
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778343"
---
# <a name="efi_usbfn_port_type"></a>EFI \_ USBFN \_ ポートの \_ 種類

この列挙体は、USB ポートの種類を指定します。

## <a name="syntax"></a>構文

```cpp
typedef enum _EFI_USBFN_PORT_TYPE
{
    EfiUsbUnknownPort = 0,
    EfiUsbStandardDownstreamPort,
    EfiUsbChargingDownstreamPort,
    EfiUsbDedicatedChargingPort,
    EfiUsbInvalidDedicatedChargingPort
} EFI_USBFN_PORT_TYPE;
```

## <a name="constants"></a>定数

| 値 | 説明 |
| --- | --- |
| EfiUsbUnknownPort | 不明なポート-ドライバー内部の既定のポートの種類。これは、成功状態コードを含むドライバーからは返されません。 |
| EfiUsbStandardDownstreamPort | 標準ダウンストリームポート-標準 USB ホスト。 |
| EfiUsbChargingDownstreamPort | ダウンストリームポート-標準 USB ホストを充電しています。 |
| EfiUsbDedicatedChargingPort | 専用充電ポート– USB ホストではなく、壁面チャージャーです。 |
| EfiUsbInvalidDedicatedChargingPort | 無効な専用充電ポート-USB ホストまたは専用の充電ポートではありません。 |

## <a name="remarks"></a>解説

詳細については、 [USB.org](https://www.usb.org/documents) web サイトの「バッテリ充電仕様、リビジョン1.1」を参照してください。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
