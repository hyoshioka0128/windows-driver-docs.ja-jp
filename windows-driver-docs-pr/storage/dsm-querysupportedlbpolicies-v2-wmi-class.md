---
title: DSM\_QuerySupportedLBPolicies\_V2 WMI クラス
description: DSM\_QuerySupportedLBPolicies\_V2 WMI クラス
ms.assetid: d60cf06d-595b-425d-bf22-f0986267ba09
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d05015071060fd7dc3c872c44c723c0600504531
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368223"
---
# <a name="dsmquerysupportedlbpoliciesv2-wmi-class"></a>DSM\_QuerySupportedLBPolicies\_V2 WMI クラス


MPIO DSM の発行\_QuerySupportedLBPolicies\_V2 WMI クラスには、GUID を登録して、その実装を処理する DSM が必要です。 DSM を使用する WMI クライアント\_QuerySupportedLBPolicies\_DSM をサポートするすべての負荷分散ポリシーを照会する V2 WMI クラスです。

```cpp
class DSM_QuerySupportedLBPolicies_V2
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
    DSM_Load_Balance_Policy_V2 Supported_LB_Policies[];
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_QuerySupportedLBPolicies\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_dsm_querysupportedlbpolicies_v2)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





