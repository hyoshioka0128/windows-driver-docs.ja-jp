---
title: ISCSI\_パス WMI クラス
description: ISCSI\_パス WMI クラス
ms.assetid: d4067869-2c67-42d3-988e-af825549853d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b9a3c1dad6878eba817bf4ceb7bf23419ab89e8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577678"
---
# <a name="iscsipath-wmi-class"></a>ISCSI\_パス WMI クラス


ISCSI\_パス WMI クラスには、iSCSI ポータルの接続に関する情報が含まれています。 このクラスが次のように定義されている*Mgmt.mof します。*

```cpp
class ISCSI_Path
{
    [WmiDataId(1),
     Description("iSCSI Unique connection id") : amended
    ]
    uint64 UniqueConnectionId;

    [WmiDataId(2),
     Description("Estimated speed of the connection in MegaBits Per Second") : amended
    ]
    uint64 EstimatedLinkSpeed;

    [WmiDataId(3),
     Description("Weight assigned to the path") : amended
    ]
    uint32 PathWeight;

    [WmiDataId(4),
     Description("Flag set to 1 if the path is a primary path, 0 otherwise.") : amended
    ]
    uint32 PrimaryPath;

    [WmiDataId(5),
     Description("Status of the path - connected, disconnected, reconnecting") : amended,
     Values{"Connected",
            "Disconnected",
            "Reconnecting"} : amended,
     DefineValues{"CONNECTION_STATE_CONNECTED",
                  "CONNECTION_STATE_DISCONNECTED",
                  "CONNECTION_STATE_RECONNECTING"
                 },
     ValueMap{"1", "2", "3"}
    ]
    uint32 ConnectionStatus;

    [WmiDataId(6),
     Description("Flag set to 1 if TCP offload is supported for this connection, 0 otherwise.") : amended
    ]
    uint32 TCPOffLoadAvailable;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_パス**](https://msdn.microsoft.com/library/windows/hardware/ff561550)データ構造体。

 

 





