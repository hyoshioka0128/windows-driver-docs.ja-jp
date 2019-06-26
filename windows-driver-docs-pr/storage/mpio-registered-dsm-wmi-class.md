---
title: MPIO\_REGISTERED\_DSM WMI クラス
description: MPIO\_REGISTERED\_DSM WMI クラス
ms.assetid: 3be335bd-e5d8-4611-9ccf-bd7fb0457b61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dc5270747e93080250298617e67fe566043065d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386145"
---
# <a name="mpioregistereddsm-wmi-class"></a>MPIO\_REGISTERED\_DSM WMI クラス


WMI クライアントが、MPIO を使用して\_登録されている\_DSM WMI クラスは、システムで構成されているすべての DSMs のクエリを実行します。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_REGISTERED\_DSM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_registered_dsm)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





