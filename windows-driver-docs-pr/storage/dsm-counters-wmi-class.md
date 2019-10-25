---
title: DSM\_カウンター WMI クラス
description: DSM\_カウンター WMI クラス
ms.assetid: 11ff77d7-5643-45ec-ac38-26ee70e6ea94
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 774cdc3543e858f38fa887b32a198a39b616fc69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845165"
---
# <a name="dsm_counters-wmi-class"></a>DSM\_カウンター WMI クラス


MPIO ドライバーは DSM\_カウンター WMI クラスを使用して、DSM に関連付けられているすべてのタイマー値を識別します。

```cpp
class DSM_COUNTERS
{
    //
    // Flag indicating if automatic path verification must be performed every
    // N seconds (where N depends on the value set in PathVerificationPeriod).
    // Type is boolean and must be filled with either 0 (disbale) or 1 (enable).
    //
    [WmiDataId(1)] uint32 PathVerifyEnabled;

    //
    // This timer is specified in seconds. It controls the periodicity
    // for path verification.
    //
    [WmiDataId(2)] uint32 PathVerificationPeriod;

    //
    // This timer is specified in seconds. It controls the amount of time
    // that the pseudo-LUN will continue to be in memory, even after
    // loosing all its paths.
    //
    [WmiDataId(3)] uint32 PDORemovePeriod;

    //
    // The number of times a failed I/O will be retried if DsmInterpretError
    // requests a retry.
    //
    [WmiDataId(4)] uint32 RetryCount;

    //
    // This value is specified in seconds. It controls the interval of time
    // after which a failed request is retried (after the DSM has decided so).
    //
    [WmiDataId(5)] uint32 RetryInterval;

    //
    // Reserved for future use.
    //
    [WmiDataId(6)] uint32 Reserved32;
    [WmiDataId(7)] uint64 Reserved64;

};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**DSM\_カウンター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_counters)のデータ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





