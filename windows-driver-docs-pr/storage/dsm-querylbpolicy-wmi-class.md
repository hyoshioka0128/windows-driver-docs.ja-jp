---
title: DSM\_QueryLBPolicy WMI クラス
description: DSM\_QueryLBPolicy WMI クラス
ms.assetid: b7fc0d38-feaa-46c5-bcde-fcd6c71b329b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ecbe83523cf8215093c64f34e2081232e2e31dc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844567"
---
# <a name="dsm_querylbpolicy-wmi-class"></a>DSM\_QueryLBPolicy WMI クラス


MPIO は DSM\_QUERYLBPolicy\_V2 WMI クラスを発行しますが、DSM が GUID を登録し、その実装を処理することを想定しています。 WMI クライアントは、DSM\_QUERYLBPolicy\_V2 WMI クラスを使用して、MPIO ディスクに設定されている負荷分散ポリシーに対してクエリを実行します。

```cpp
class DSM_QueryLBPolicy
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    [WmiDataId(1),
     DisplayName("Load Balance Policy") : amended,
     Description("Load Balance Policy that is currently being used by DSM") : amended
    ]
    DSM_Load_Balance_Policy LoadBalancePolicy;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**DSM\_QueryLBPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querylbpolicy)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





