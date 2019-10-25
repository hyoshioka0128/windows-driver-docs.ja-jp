---
title: MSiSCSI\_LB\_Operations WMI クラス
description: MSiSCSI\_LB\_Operations WMI クラス
ms.assetid: 75c93040-52bf-4e9c-a503-a87f382ee1c9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba6b6e620b2e18364132011593e40c50d8cd25d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845350"
---
# <a name="msiscsi_lb_operations-wmi-class"></a>MSiSCSI\_LB\_Operations WMI クラス


MSiSCSI\_LB\_Operations WMI クラスには、負荷分散ポリシーを設定および取得するメソッドが含まれています。 このクラスは、管理 .mof で次のように定義されています。

```cpp
class MSiSCSI_LB_Operations {

    [key, read]
    string InstanceName;

    [read] 
    boolean Active;

    //
    // Method to set load balance policy for the iSCSI Initiator
    //
    [WmiMethodId(10),
     Implemented,
     Description("Sets Load Balance Policy for the iSCSI Initiator") : amended,
     cpp_quote(
       "//\n"
       "// SetLoadBalancePolicy instructs the iSCSI Initiator what Load Balance\n"
       "// policy to use.\n"
       "//\n"
              )            
    ]
    void SetLoadBalancePolicy(
        [in,
         Description("New Load Balance policy to be set")
        ] ISCSI_Supported_LB_Policies LoadBalancePolicies,

        [out,
         Description("Status of the operation")
        ] uint32 Status
    );
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [Msiscsi\_LB\_操作](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)データ構造体の1つを生成します。

 

 





