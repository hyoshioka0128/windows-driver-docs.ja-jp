---
title: DSM\_QueryLBPolicy\_V2 WMI クラス
description: DSM\_QueryLBPolicy\_V2 WMI クラス
ms.assetid: 748db832-9ddb-4ca0-a229-9f5d95f5c24b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d1e7c77784431af2c84d3e0b82e12cae3ea4273
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844569"
---
# <a name="dsm_querylbpolicy_v2-wmi-class"></a>DSM\_QueryLBPolicy\_V2 WMI クラス


MPIO は DSM\_QUERYLBPolicy\_V2 WMI クラスを発行しますが、DSM が GUID を登録し、その実装を処理することを想定しています。 WMI クライアントは、DSM\_QUERYLBPolicy\_V2 WMI クラスを使用して、MPIO ディスクに設定されている負荷分散ポリシーを照会します。

```cpp
class DSM_QueryLBPolicy_V2
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    [WmiDataId(1),
     DisplayName("Load Balance Policy") : amended,
     Description("Load Balance Policy that is currently being used by DSM") : amended
    ]
    DSM_Load_Balance_Policy_V2 LoadBalancePolicy;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**DSM\_QueryLBPolicy\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querylbpolicy_v2)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





