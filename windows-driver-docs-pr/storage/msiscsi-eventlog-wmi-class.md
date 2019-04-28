---
title: MSiSCSI\_EventLog WMI クラス
description: MSiSCSI\_EventLog WMI クラス
ms.assetid: 8fe6c3fd-bb4f-46ac-a69c-5508467b4c70
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e2f2c780594c1eba0a765725d96d68c4656dd9a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361714"
---
# <a name="msiscsieventlog-wmi-class"></a>MSiSCSI\_EventLog WMI クラス


MSiSCSI\_システム イベント ログに、iSCSI イベントをログにイベント ログの WMI クラスを使用します。 このクラスが次のように定義されている*Mgmt.mof します。*

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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_EventLog** ](https://msdn.microsoft.com/library/windows/hardware/ff563001)データ構造体。

 

 





