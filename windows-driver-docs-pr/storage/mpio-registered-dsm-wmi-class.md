---
title: MPIO\_\_DSM WMI クラスに登録されています
description: MPIO\_\_DSM WMI クラスに登録されています
ms.assetid: 3be335bd-e5d8-4611-9ccf-bd7fb0457b61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cb832ee0201ae52fc9207244098a92bc3d833037
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843567"
---
# <a name="mpio_registered_dsm-wmi-class"></a>MPIO\_\_DSM WMI クラスに登録されています


WMI クライアントは、システムで構成されているすべての dsm を照会するために、\_DSM WMI クラスに登録されている MPIO\_を使用します。

```cpp
class MPIO_REGISTERED_DSM
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // The Number of DSMs that have registered with MPIO.
    //
    [WmiDataId(1),
     read,
     Description("Number of registered DSMs.") : amended
    ] uint32 NumberDSMs;

    //
    // Variable-length array of DSM_PARAMETERS structures.
    // NOTE: Each entry will be ULONG aligned. App. writers
    // take note when iterating through the array.
    //
    [WmiDataId(2),
     read,
     Description("Counters information of registered DSMs.") : amended,
     WmiSizeIs("NumberDSMs")
    ] DSM_PARAMETERS DsmParameters[];
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**DSM データ構造\_登録された MPIO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_registered_dsm)生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





