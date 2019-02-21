---
title: DSM\_QueryLBPolicy\_V2 WMI クラス
description: DSM\_QueryLBPolicy\_V2 WMI クラス
ms.assetid: 748db832-9ddb-4ca0-a229-9f5d95f5c24b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 05411785eae164ada0dec55aa3fbbd5116b97052
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527417"
---
# <a name="dsmquerylbpolicyv2-wmi-class"></a>DSM\_QueryLBPolicy\_V2 WMI クラス


MPIO DSM の発行\_QUERYLBPolicy\_V2 WMI クラスには、GUID を登録して、その実装を処理する DSM が必要です。 DSM を使用する WMI クライアント\_QUERYLBPolicy\_V2 WMI クラスは、クエリ、MPIO ディスクに対して設定されている負荷分散ポリシーです。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_QueryLBPolicy\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff552724)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





