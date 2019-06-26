---
title: MPIO\_DSM\_パス WMI クラス
description: MPIO\_DSM\_パス WMI クラス
ms.assetid: 4f8d7fb0-2b9a-44dc-bb87-f70285f1b47c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7df5c8c9de117e5b2c0aab6e1c5c89fc4a502265
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386159"
---
# <a name="mpiodsmpath-wmi-class"></a>MPIO\_DSM\_パス WMI クラス


MPIO の発行、MPIO\_DSM\_パス\_V2 WMI クラスには、GUID を登録して、その実装を処理する DSM が必要です。 MPIO ドライバーは、MPIO を使用して\_DSM\_パス\_V2 WMI クラス、DSM で報告されたパスの ID を識別するためにします。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_DSM\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_mpio_dsm_path)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





