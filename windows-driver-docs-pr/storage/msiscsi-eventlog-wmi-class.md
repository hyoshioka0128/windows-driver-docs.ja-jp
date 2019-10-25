---
title: MSiSCSI\_EventLog WMI クラス
description: MSiSCSI\_EventLog WMI クラス
ms.assetid: 8fe6c3fd-bb4f-46ac-a69c-5508467b4c70
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7314dc2f51836e253acb1fe689a1af6d19173b7a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845365"
---
# <a name="msiscsi_eventlog-wmi-class"></a>MSiSCSI\_EventLog WMI クラス


MSiSCSI\_EventLog WMI クラスは、任意の iSCSI イベントをシステムイベントログに記録するために使用されます。 このクラスは、管理 .mof で次のように定義されてい*ます。*

```cpp
class MSiSCSI_Eventlog : __ExtrinsicEvent
{
    [key] 
    string InstanceName;
 
    boolean Active;
 
    [WmiDataId(1),
     EVENTLOG_MESSAGE_QUALIFIERS
    ]
    uint32 Type;

    [WmiDataId(2),
     Description("If zero, then this event is not logged to system eventlog") : amended
    ]
    uint32 LogToEventlog;

    [WmiDataId(3),
     Description("Size of Additional Data") : amended
    ]
    uint32 Size;

    [WmiDataId(4),
     WmiSizeIs("Size"),
     Description("Additional data to include in eventlog message, typically iSCSI Header") : amended
    ]
    uint8 AdditionalData[];    
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_EventLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_eventlog)データ構造を生成します。

 

 





