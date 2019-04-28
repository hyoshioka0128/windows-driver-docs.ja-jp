---
title: MPIO\_REGISTERED\_DSM WMI クラス
description: MPIO\_REGISTERED\_DSM WMI クラス
ms.assetid: 3be335bd-e5d8-4611-9ccf-bd7fb0457b61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2a0bc7e71000eba08061c133e8062e9e902ba080
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383046"
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_REGISTERED\_DSM** ](https://msdn.microsoft.com/library/windows/hardware/ff562449)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





