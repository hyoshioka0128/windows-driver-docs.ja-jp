---
title: ISCSI\_サポート\_LB\_ポリシー WMI クラス
description: ISCSI\_サポート\_LB\_ポリシー WMI クラス
ms.assetid: c11eebe8-519a-473d-9e9c-8a787333223e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 36df0a2a5921c602f80206ec73bbdf9ebb83bdc6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366120"
---
# <a name="iscsisupportedlbpolicies-wmi-class"></a>ISCSI\_サポート\_LB\_ポリシー WMI クラス


ISCSI\_サポートされている\_LB\_ポリシー WMI クラスには、複数の接続の iSCSI セッションのサポートされている負荷分散ポリシーに関する情報が含まれています。 このクラスが次のように定義されている*Mgmt.mof します。*

```cpp
class ISCSI_Supported_LB_Policies {

    [WmiDataId(1),
     description("Id that is unique to this session within this adapter. ") : amended
    ]
    uint64 UniqueSessionId;

    [WmiDataId(2),
     Description("Load Balance policy supported by the iSCSI Initiator") : amended,
     Values{"Fail Over Only",
            "Round Robin",
            "Round Robin with Subset",
            "Dynamic Least Queue Depth",
            "Weighted Paths",
            "Vendor Specific"} : amended,
     DefineValues{"MSiSCSI_LB_FAILOVER",
                  "MSiSCSI_LB_ROUND_ROBIN",
                  "MSiSCSI_LB_ROUND_ROBIN_WITH_SUBSET",
                  "MSiSCSI_LB_DYN_LEAST_QUEUE_DEPTH",
                  "MSiSCSI_LB_WEIGHTED_PATHS",
                  "MSiSCSI_LB_VENDOR_SPECIFIC"},
     ValueMap{"1", "2", "3", "4", "5", "6"}
    ] 
    uint32 LoadBalancePolicy;
 
    //
    // If load balance policy is MSiSCSI_LB_VENDOR_SPECIFIC then 
    // the following properties are not used. Instead the caller would 
    // need to provide data for setting the vendor specific
    // Load Balance policy.
    //
    [WmiDataId(3),
     Description("Number of entries in MSiSCSI_Paths array") : amended
    ]

    uint32 iSCSI_PathCount;

    [WmiDataId(4),
     WmiSizeIs("iSCSI_PathCount"),
     Description("Describes iSCSI Initiator Paths") : amended
    ]
    ISCSI_Path iSCSI_Paths[];
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_サポートされている\_LB\_ポリシー** ](https://msdn.microsoft.com/library/windows/hardware/ff561570)データ構造体。

 

 





