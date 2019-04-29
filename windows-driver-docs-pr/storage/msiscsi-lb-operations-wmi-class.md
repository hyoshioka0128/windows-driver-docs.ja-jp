---
title: MSiSCSI\_LB\_操作 WMI クラス
description: MSiSCSI\_LB\_操作 WMI クラス
ms.assetid: 75c93040-52bf-4e9c-a503-a87f382ee1c9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2e82438bad7380656e9bea8e031966b1c4cad3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329614"
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

1 つ生成 WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに、 [MSiSCSI\_LB\_操作](https://msdn.microsoft.com/library/windows/hardware/ff563059)データ構造体。

 

 





