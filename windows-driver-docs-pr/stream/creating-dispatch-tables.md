---
title: ディスパッチ テーブルの作成
description: ディスパッチ テーブルの作成
ms.assetid: 0771aeac-68b2-4dec-8887-a0b313899ce8
keywords:
- BDA ミニドライバー WDK AVStream、ディスパッチテーブル
- ディスパッチテーブル WDK AVStream
- ディスパッチテーブルのフィルター WDK BDA
- ディスパッチテーブルの固定 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b99f1ad4614e0152f59bb9f97c3315a90e5dc137
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827124"
---
# <a name="creating-dispatch-tables"></a>ディスパッチ テーブルの作成





ネットワークプロバイダーフィルターがフィルターのインスタンスを開いて初期化し、後でフィルターインスタンスを解放できるように、BDA ミニドライバーのフィルター記述子 ([**Ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)) のフィルターディスパッチテーブルを作成する必要があります。 また、フィルターのテンプレートトポロジで使用できるピンの種類の配列で、各 pin 記述子 ([**Kspin\_descriptor\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)) のピンディスパッチテーブルを作成する必要があります。 ネットワークプロバイダーフィルターは、pin ディスパッチテーブルを使用して pin を開いて初期化し、後で pin を解放します。 次のコードスニペットは、フィルターおよびピンディスパッチテーブルの例を示しています。

```cpp
//
//  Filter Dispatch Table
//
//  Lists the dispatch routines for major events at the filter
//  level.
//
const
KSFILTER_DISPATCH
FilterDispatch =
{
    CFilter::Create,        // Create
    CFilter::FilterClose,   // Close
    NULL,                   // Process
    NULL                    // Reset
};

//
//  Input Pin Dispatch Table
//  Lists the dispatch routines for major events at the pin level.
//
const
KSPIN_DISPATCH
AntennaPinDispatch =
{
    CAntennaPin::PinCreate,         // Create
    CAntennaPin::PinClose,          // Close
    NULL,                           // Process signal data
    NULL,                           // Reset
    NULL,                           // SetDataFormat
    CAntennaPin::PinSetDeviceState, // SetDeviceState
    NULL,                           // Connect
    NULL,                           // Disconnect
    NULL,                           // Clock
    NULL                            // Allocator
};
```

 

 




