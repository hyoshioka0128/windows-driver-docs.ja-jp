---
title: DSM\_QuerySupportedLBPolicies\_V2 WMI クラス
description: DSM\_QuerySupportedLBPolicies\_V2 WMI クラス
ms.assetid: d60cf06d-595b-425d-bf22-f0986267ba09
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7cb3467ecc565e42f1bb1d9703d88ffdb799e0fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843221"
---
# <a name="dsm_querysupportedlbpolicies_v2-wmi-class"></a>DSM\_QuerySupportedLBPolicies\_V2 WMI クラス


MPIO は DSM\_QuerySupportedLBPolicies\_V2 WMI クラスを発行しますが、DSM が GUID を登録し、その実装を処理することを想定しています。 WMI クライアントは DSM\_QuerySupportedLBPolicies\_V2 WMI クラスを使用して、DSM がサポートする負荷分散ポリシーをすべて照会します。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**DSM\_QuerySupportedLBPolicies\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querysupportedlbpolicies_v2)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





