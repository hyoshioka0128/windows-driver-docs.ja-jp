---
title: DSM\_ロード\_残高\_ポリシー WMI クラス
description: DSM\_ロード\_残高\_ポリシー WMI クラス
ms.assetid: 7de58fe6-7c95-412a-9135-3894c07137a7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dfd2e1d024a66aae0079b8649a643c76a11dbac6
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349297"
---
# <a name="dsmloadbalancepolicy-wmi-class"></a>DSM\_ロード\_残高\_ポリシー WMI クラス


MPIO DSM の発行\_ロード\_残高\_ポリシー\_V2 WMI クラスには、GUID を登録して、その実装を処理する DSM が必要です。 MPIO ドライバーは DSM を使用して\_読み込む\_残高\_ポリシー\_V2 WMI クラス、MPIO ディスクに適用される負荷分散ポリシーを識別するためにします。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_ロード\_残高\_ポリシー** ](https://msdn.microsoft.com/library/windows/hardware/ff552696)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





