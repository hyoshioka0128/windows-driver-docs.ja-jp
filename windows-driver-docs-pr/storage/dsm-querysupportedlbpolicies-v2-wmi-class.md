---
title: DSM\_QuerySupportedLBPolicies\_V2 WMI クラス
description: DSM\_QuerySupportedLBPolicies\_V2 WMI クラス
ms.assetid: d60cf06d-595b-425d-bf22-f0986267ba09
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5fc77b00fb66022c4aaa8cff6f2a41aa179a0c48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529692"
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_QuerySupportedLBPolicies\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff552735)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





