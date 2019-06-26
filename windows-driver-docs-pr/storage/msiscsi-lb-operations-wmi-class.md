---
title: MSiSCSI\_LB\_操作 WMI クラス
description: MSiSCSI\_LB\_操作 WMI クラス
ms.assetid: 75c93040-52bf-4e9c-a503-a87f382ee1c9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 129fd5aa321ce8e68c613a6b896508d78ff1ac82
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370433"
---
# <a name="msiscsilboperations-wmi-class"></a>MSiSCSI\_LB\_操作 WMI クラス


MSiSCSI\_LB\_操作 WMI クラスに設定し、負荷分散ポリシーを取得するメソッドが含まれています。 このクラスは、Mgmt.mof で次のように定義されます。

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

1 つ生成 WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに、 [MSiSCSI\_LB\_操作](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)データ構造体。

 

 





