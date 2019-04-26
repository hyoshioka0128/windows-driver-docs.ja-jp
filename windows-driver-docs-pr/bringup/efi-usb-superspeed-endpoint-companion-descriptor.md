---
title: EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR
description: EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR
ms.assetid: 5449A10A-17BC-40CB-A8FC-19F867CFC9D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4f5536405e92ac5b1b938f4c60389a09c92f051
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337774"
---
# <a name="efiusbsuperspeedendpointcompaniondescriptor"></a>EFI\_USB\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子


**EFI\_USB\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子**構造体は、USB 関数に SuperSpeed エンドポイント コンパニオンの記述子を提供します。ドライバー。

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


<a href="" id="length"></a>**長さ**  
この記述子 (バイト単位) のサイズ。

<a href="" id="descriptortype"></a>**DescriptorType**  
記述子の型を指定します。 SUPERSPEED に設定する必要があります\_USB\_エンドポイント\_付属します。

<a href="" id="maxburst"></a>**MaxBurst**  
エンドポイントは送信したり、バーストの一部として受信パケットの最大数。

<a href="" id="asuchar"></a>**AsUchar**  
構造体の長さを指定します。

<a href="" id="maxstreams"></a>**MaxStreams**  
一括エンドポイントでサポートされているストリームの最大数を指定します。

<a href="" id="reserved1"></a>**Reserved1**  
予約済み。 使わないでください。

<a href="" id="bytesperinterval"></a>**BytesPerInterval**  
合計数バイトのこのエンドポイントは、すべてのサービス期間 (SI) に転送します。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




