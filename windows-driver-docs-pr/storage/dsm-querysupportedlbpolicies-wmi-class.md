---
title: DSM\_QuerySupportedLBPolicies WMI クラス
description: DSM\_QuerySupportedLBPolicies WMI クラス
ms.assetid: fab4d9e6-68fb-42f8-89e5-a5f5b2580964
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dc52fd9ac4aad75674d84366c760103af25e60e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368226"
---
# <a name="dsmquerysupportedlbpolicies-wmi-class"></a>DSM\_QuerySupportedLBPolicies WMI クラス


MPIO DSM の発行\_QuerySupportedLBPolicies\_V2 WMI クラスには、GUID を登録して、その実装を処理する DSM が必要です。 DSM を使用する WMI クライアント\_QuerySupportedLBPolicies\_DSM をサポートするすべての負荷分散ポリシーを照会する V2 WMI クラスです。

```cpp
class DSM_QuerySupportedLBPolicies
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    [WmiDataId(1),
     Description("Number of supported Load Balance policies") : amended
    ]
    uint32 SupportedLBPoliciesCount;

    [WmiDataId(2),
     Description("Reserved") : amended
    ]
    uint32 Reserved;

    [WmiDataId(3),
     WmiSizeIs("SupportedLBPoliciesCount"),
     Description("Supported Load Balance Policies array") : amended
    ]
    DSM_Load_Balance_Policy Supported_LB_Policies[];
};
```

ときにこのクラスは、WMI ツール スイートによってコンパイルの定義に、このクラス定義で生成、 [ **DSM\_QuerySupportedLBPolicies** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_dsm_querysupportedlbpolicies)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





