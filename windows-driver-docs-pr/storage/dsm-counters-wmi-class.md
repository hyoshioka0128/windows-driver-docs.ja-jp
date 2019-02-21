---
title: DSM\_カウンター WMI クラス
description: DSM\_カウンター WMI クラス
ms.assetid: 11ff77d7-5643-45ec-ac38-26ee70e6ea94
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d9a038eb06228b83f567f336d7161807ad213ef1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560268"
---
# <a name="dsmcounters-wmi-class"></a>DSM\_カウンター WMI クラス


MPIO ドライバーは DSM を使用して\_DSM に関連付けられているすべてのタイマー値を識別するカウンターの WMI クラスです。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_カウンター** ](https://msdn.microsoft.com/library/windows/hardware/ff552683)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





