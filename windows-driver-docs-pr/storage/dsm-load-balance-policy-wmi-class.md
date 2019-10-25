---
title: DSM\_負荷\_分散\_ポリシー WMI クラス
description: DSM\_負荷\_分散\_ポリシー WMI クラス
ms.assetid: 7de58fe6-7c95-412a-9135-3894c07137a7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 17364de21af53a127627fe236a20a53a6e9be5cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833821"
---
# <a name="dsm_load_balance_policy-wmi-class"></a>DSM\_負荷\_分散\_ポリシー WMI クラス


MPIO は、DSM\_負荷\_バランス\_ポリシー\_V2 WMI クラスを発行しますが、DSM が GUID を登録し、その実装を処理することを想定しています。 MPIO ドライバーは、DSM\_LOAD\_の負荷分散\_ポリシー\_V2 WMI クラスを使用して、MPIO ディスクに適用されている負荷分散ポリシーを特定します。

```cpp
class DSM_Load_Balance_Policy
{

    //
    // Version information for further changes.
    //
    [WmiDataId(1),
     read,
     Description("Version Number") : amended
    ]
    uint32 Version;

    //
    // Load Balance type.
    //
    [WmiDataId(2),
     Description("Load Balance Policy implemented by the DSM") : amended,
     Values{"Fail Over Only",
            "Round Robin",
            "Round Robin with Subset",
            "Dynamic Least Queue Depth",
            "Weighted Paths",
            "Least Blocks",
            "Vendor Specific"} : amended,

     DefineValues{"DSM_LB_FAILOVER",
                  "DSM_LB_ROUND_ROBIN",
                  "DSM_LB_ROUND_ROBIN_WITH_SUBSET",
                  "DSM_LB_DYN_LEAST_QUEUE_DEPTH",
                  "DSM_LB_WEIGHTED_PATHS",
                  "DSM_LB_LEAST_BLOCKS",
                  "DSM_LB_VENDOR_SPECIFIC"},
     ValueMap{"1", "2", "3", "4", "5", "6", "7"}
    ]
    uint32 LoadBalancePolicy;

    //
    // If load balance policy is DSM_LB_VENDOR_SPECIFIC then the following
    // properties are not used. The caller would need to provide data for
    // setting the vendor specific Load Balance policy.
    //

    //
    // Number of paths.
    //
    [WmiDataId(3),
     Description("Number of entries in DSM_Paths array") : amended
    ]
    uint32 DSMPathCount;

    [WmiDataId(4),
     Description("Reserved field") : amended
    ]
    uint32 Reserved;

    //
    // Paths' array.
    //
    [WmiDataId(5),
     WmiSizeIs("DSMPathCount"),
     Description("DSM_Paths array") : amended
    ]
    MPIO_DSM_Path DSM_Paths[];
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、ポリシーのデータ構造[ **\_の負荷\_分散\_DSM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_load_balance_policy)が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





