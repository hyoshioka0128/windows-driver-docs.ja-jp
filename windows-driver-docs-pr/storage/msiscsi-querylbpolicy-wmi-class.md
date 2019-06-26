---
title: MSiSCSI\_QueryLBPolicy WMI クラス
description: MSiSCSI\_QueryLBPolicy WMI クラス
ms.assetid: 1d80f525-491a-4c81-8827-7c5c13107a54
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8296f46960aadd706e613bec2788dfee3d412be5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384683"
---
# <a name="msiscsiquerylbpolicy-wmi-class"></a>MSiSCSI\_QueryLBPolicy WMI クラス


MSiSCSI\_QueryLBPolicy WMI クラスには、負荷分散ポリシーに関する情報が含まれています。 このクラスが次のように定義されている*Mgmt.mof します。*

```cpp
class MSiSCSI_QueryLBPolicy 
{
    [key]
    string InstanceName;

    boolean Active;

    [WmiDataId(1),
     DisplayName("Adapter Id") : amended,
     DisplayInHex,
     Description("Id that is globally unique to each instance of each adapter. Using the address of the Adapter Extension is a good idea.") : amended
    ]
    uint64 UniqueAdapterId;

    [WmiDataId(2),
     read,
     DisplayName("Reserved field") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     DisplayName("Count of Elements in LoadBalancePolicies array") : amended,
     cpp_quote("\n    // Number of elements in LoadBalancePolicies array\n"),
     Description("Number of elements in LoadBalancePolicies array") : amended
    ] uint32 SessionCount;

    [WmiDataId(4),
     DisplayName("Load Balance Policy for each session") : amended,
     description("Load Balance Policy that is currently being used by iSCSI Initiator - one element for each session on the adapter") : amended,
     WmiSizeIs("SessionCount")
    ]
    ISCSI_Supported_LB_Policies LoadBalancePolicies[];
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_QueryLBPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_msiscsi_querylbpolicy)データ構造体。

 

 





