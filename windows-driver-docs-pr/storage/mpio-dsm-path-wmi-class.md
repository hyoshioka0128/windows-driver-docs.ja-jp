---
title: MPIO\_DSM\_パス WMI クラス
description: MPIO\_DSM\_パス WMI クラス
ms.assetid: 4f8d7fb0-2b9a-44dc-bb87-f70285f1b47c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5a073c5e30b8196db7b84056852a83af1dd81830
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843569"
---
# <a name="mpio_dsm_path-wmi-class"></a>MPIO\_DSM\_パス WMI クラス


Mpio は、MPIO\_DSM\_Path\_V2 WMI クラスを発行しますが、DSM が GUID を登録し、その実装を処理することを想定しています。 MPIO ドライバーは、MPIO\_DSM\_Path\_V2 WMI クラスを使用して、DSM によって報告されたパス ID を識別します。

```cpp
class MPIO_DSM_Path
{

    //
    // Unique identifier to distinguish paths known to the DSM.
    // This is what is returned to MPIO during DsmSetDeviceInfo.
    //
    [WmiDataId(1),
     Description("DSM Path Id") : amended
    ]
    uint64 DsmPathId;

    //
    // Reserved.
    //
    [WmiDataId(2),
     Description("Reserved field") : amended
    ]
    uint64 Reserved;

    //
    // Value that determines which path the DSM picks if the load balance is
    // Weighted Paths.
    //
    [WmiDataId(3),
     Description("Weight assigned to the path") : amended
    ]
    uint32 PathWeight;

    //
    // Flag to indicate if this is a primary path.
    //
    [WmiDataId(4),
     Description("Flag set to TRUE if the path is a primary path. Else FALSE.") : amended
    ]
    uint32 PrimaryPath;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_DSM\_Path**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_mpio_dsm_path)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





