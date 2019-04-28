---
title: ディスパッチ テーブルの作成
description: ディスパッチ テーブルの作成
ms.assetid: 0771aeac-68b2-4dec-8887-a0b313899ce8
keywords:
- BDA ミニドライバー WDK AVStream、ディスパッチ テーブル
- ディスパッチ テーブル WDK AVStream
- ディスパッチ テーブル WDK BDA をフィルター処理します。
- ピン留めするディスパッチ テーブル WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab3da16f49a1cae0dcb8002623dd039305d93df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374169"
---
# <a name="creating-dispatch-tables"></a>ディスパッチ テーブルの作成





フィルター記述子のフィルターのディスパッチ テーブルを作成する必要があります ([**KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)) BDA ミニドライバーのネットワーク プロバイダーのフィルターを開きのインスタンスを初期化できるように、フィルター処理し、フィルターのインスタンスを後でリリースします。 各ピン記述子のピン留めするディスパッチ テーブルを作成することも必要があります ([**KSPIN\_記述子\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)) で、フィルターのテンプレートのトポロジで使用可能な暗証番号 (pin) 型の配列. ネットワーク プロバイダーのフィルターでは、暗証番号 (pin) のディスパッチ テーブルを使用して、開き、pin を初期化し、pin を後でリリースします。 次のコード スニペットでは、フィルターと pin のディスパッチ テーブルの例を示します。

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

 

 




