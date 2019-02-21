---
title: DSM\_QuerySupportedLBPolicies WMI クラス
description: DSM\_QuerySupportedLBPolicies WMI クラス
ms.assetid: fab4d9e6-68fb-42f8-89e5-a5f5b2580964
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eb980544740617b6a55aa812faeba8c4e4fcb24a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530842"
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

ときにこのクラスは、WMI ツール スイートによってコンパイルの定義に、このクラス定義で生成、 [ **DSM\_QuerySupportedLBPolicies** ](https://msdn.microsoft.com/library/windows/hardware/ff552733)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





