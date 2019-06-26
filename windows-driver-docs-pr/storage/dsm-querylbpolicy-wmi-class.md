---
title: DSM\_QueryLBPolicy WMI クラス
description: DSM\_QueryLBPolicy WMI クラス
ms.assetid: b7fc0d38-feaa-46c5-bcde-fcd6c71b329b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9dfe9b155880d968a180877bd44f0e5e2850b9be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368236"
---
# <a name="dsmquerylbpolicy-wmi-class"></a>DSM\_QueryLBPolicy WMI クラス


MPIO DSM の発行\_QUERYLBPolicy\_V2 WMI クラスには、GUID を登録して、その実装を処理する DSM が必要です。 DSM を使用する WMI クライアント\_QUERYLBPolicy\_MPIO ディスクの負荷分散ポリシーを照会する V2 WMI クラスを設定します。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_QueryLBPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_dsm_querylbpolicy)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





