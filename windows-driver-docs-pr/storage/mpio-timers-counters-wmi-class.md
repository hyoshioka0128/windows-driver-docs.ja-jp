---
title: MPIO\_タイマー\_カウンター WMI クラス
description: MPIO\_タイマー\_カウンター WMI クラス
ms.assetid: 386110f8-504c-4617-b8ae-557ea504d41d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4590a37632bed94ce62f1ad86c3d8bd5822118d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386150"
---
# <a name="mpiotimerscounters-wmi-class"></a>MPIO\_タイマー\_カウンター WMI クラス


WMI クライアントが、MPIO を使用して\_タイマー\_カウンター WMI クラスのすべてのグローバルなタイマー値 MPIO をクエリします。

```cpp
class MPIO_TIMERS_COUNTERS
{

    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Flag indicating if automatic path verification must be performed every
    // N seconds (where N depends on the value set in PathVerificationPeriod).
    // Type is boolean and must be filled with either 0 (disbale) or 1 (enable).
    //
    [WmiDataId(1),
     read, write,
     Description("Enable/Disable Auto Path-Verification.") : amended
    ] uint32 PathVerifyEnabled;

    //
    // This timer is specified in seconds. The default is 30 seconds
    // and its max allowed is MAXULONG. It controls the periodicity
    // for path verification.
    //
    [WmiDataId(2),
     read, write,
     Description("Path Verification Timer.") : amended
    ] uint32 PathVerificationPeriod;

    //
    // This timer is specified in seconds. The default is 20 seconds
    // and its max allowed is MAXULONG. It controls the amount of time
    // that the pseudo-LUN will continue to be in memory, even after
    // loosing all its paths.
    //
    [WmiDataId(3),
     read, write,
     Description("PDO Remove Timer.") : amended
    ] uint32 PDORemovePeriod;

    //
    // The number of times a failed I/O will be retried if DsmInterpretError
    // requests a retry. The default is set to 3.
    //
    [WmiDataId(4),
     read, write,
     Description("Request Retry Count (Max 500)") : amended
    ] uint32 RetryCount;

    //
    // This value is specified in seconds. The default is 1 second. It
    // controls the interval of time after which a failed request is
    // retried (after the DSM has decided so).
    //
    [WmiDataId(5),
     read, write,
     Description("Retry Interval (seconds) (Max MAXULONG)") : amended
    ] uint32 RetryInterval;

};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_タイマー\_カウンター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_timers_counters)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





