---
title: ISCSI\_パス WMI クラス
description: ISCSI\_パス WMI クラス
ms.assetid: d4067869-2c67-42d3-988e-af825549853d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b3acf193ce8e941cc108bfc0ab288d9ed8dac9b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842264"
---
# <a name="iscsi_path-wmi-class"></a>ISCSI\_パス WMI クラス


ISCSI\_Path WMI クラスには、iSCSI ポータルの接続に関する情報が含まれています。 このクラスは、管理 .mof で次のように定義されてい*ます。*

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

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**ISCSI\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_path)のデータ構造を生成します。

 

 





