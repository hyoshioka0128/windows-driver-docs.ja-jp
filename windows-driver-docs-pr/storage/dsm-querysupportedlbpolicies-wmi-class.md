---
title: DSM\_QuerySupportedLBPolicies WMI クラス
description: DSM\_QuerySupportedLBPolicies WMI クラス
ms.assetid: fab4d9e6-68fb-42f8-89e5-a5f5b2580964
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 608a772016787ceb475b122eb85551a3cac9e5a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844565"
---
# <a name="dsm_querysupportedlbpolicies-wmi-class"></a>DSM\_QuerySupportedLBPolicies WMI クラス


MPIO は DSM\_QuerySupportedLBPolicies\_V2 WMI クラスを発行しますが、DSM が GUID を登録し、その実装を処理することを想定しています。 WMI クライアントは DSM\_QuerySupportedLBPolicies\_V2 WMI クラスを使用して、DSM がサポートする負荷分散ポリシーをすべて照会します。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、このクラス定義によって[**DSM\_QuerySupportedLBPolicies**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querysupportedlbpolicies)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





