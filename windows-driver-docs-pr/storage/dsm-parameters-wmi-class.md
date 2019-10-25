---
title: DSM\_パラメーター WMI クラス
description: DSM\_パラメーター WMI クラス
ms.assetid: c946f8cb-327c-4d5a-a133-0051a405fcad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6d2a295c01a7f5b215e34d76a91f0dd830ee2c79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844571"
---
# <a name="dsm_parameters-wmi-class"></a>DSM\_パラメーター WMI クラス


MPIO ドライバーは、dsm とそれに関連付けられているすべてのタイマー値を識別するために、DSM\_パラメーター WMI クラスをユーザーに割り当てます。

```cpp
class DSM_PARAMETERS
{
    //
    // Friendly name of the registered DSM.
    //
    [WmiDataId(1), MaxLen(63)] string DsmName;

    //
    // DSM-unique handle.
    //
    [WmiDataId(2)] uint64 DsmContext;

    //
    // Version Info
    //
    [WmiDataId(3)] DSM_VERSION DsmVersion;

    //
    // Counters Info
    //
    [WmiDataId(4)] DSM_COUNTERS DsmCounters;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**DSM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_parameters)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





