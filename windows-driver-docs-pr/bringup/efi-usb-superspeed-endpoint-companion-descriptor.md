---
title: EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR
description: EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR
ms.assetid: 5449A10A-17BC-40CB-A8FC-19F867CFC9D0
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: e7e6e3d081ecb3a815a965d5773cf9a99330d281
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778331"
---
# <a name="efi_usb_superspeed_endpoint_companion_descriptor"></a>EFI \_ USB \_ SUPERSPEED \_ エンドポイント \_ コンパニオン \_ 記述子

**EFI \_ usb \_ SUPERSPEED \_ エンドポイント \_ コンパニオンの \_ 記述子**構造体は、Usb 関数ドライバーに SUPERSPEED エンドポイントコンパニオン記述子を提供します。

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    UINT8          Length;
    UINT8          DescriptorType;
    UINT8          MaxBurst;
    union
    {
        UINT8      AsUchar;
        struct
        {
            UINT8  MaxStreams:5;
            UINT8  Reserved1:3;
        }          Bulk;
    }              Attributes;
    UINT16         BytesPerInterval;
} EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR;
```

## <a name="members"></a>メンバー

### <a name="length"></a>長さ

この記述子のサイズ (バイト単位)。

### <a name="descriptortype"></a>記述子の型

記述子の種類を指定します。 SUPERSPEED \_ USB エンドポイントコンパニオンに設定する必要があり \_ \_ ます。

### <a name="maxburst"></a>MaxBurst

バーストの一部として、エンドポイントが送信または受信できるパケットの最大数。

### <a name="asuchar"></a>AsUchar

構造体の長さを指定します。

### <a name="maxstreams"></a>MaxStreams

一括エンドポイントでサポートされるストリームの最大数を指定します。

### <a name="reserved1"></a>Reserved1

予約済み。 使用しないでください。

### <a name="bytesperinterval"></a>BytesPerInterval

このエンドポイントがすべてのサービス間隔 (SI) に転送するバイト数の合計です。

## <a name="requirements"></a>要件

**ヘッダー:** ユーザーが生成
