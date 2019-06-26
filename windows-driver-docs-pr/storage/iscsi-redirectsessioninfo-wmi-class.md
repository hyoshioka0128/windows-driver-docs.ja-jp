---
title: ISCSI\_RedirectSessionInfo WMI クラス
description: ISCSI\_RedirectSessionInfo WMI クラス
ms.assetid: eb1ec866-2dcd-4099-a24f-ae1d0c702b95
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 02e743a20cc96fecbc9d0b6eee41e262c5e48e51
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378408"
---
# <a name="iscsiredirectsessioninfo-wmi-class"></a>ISCSI\_RedirectSessionInfo WMI クラス


ISCSI\_RedirectSessionInfo WMI クラスには、iSCSI セッションの接続のコレクションが含まれています。 このクラスが次のように定義されている*Mgmt.mof します。*

```cpp
class ISCSI_RedirectSessionInfo
{
    [read,
     WmiDataId(1),
     Description("A uniquely generated session ID, it is the same id returned by the LoginToTarget method.  Do not confuse this with ISID or SSID."): amended,
     WmiVersion(1)] uint64 UniqueSessionId;

    [read,
     WmiDataId(2),
     Description("Target portal group tag for this Session "): amended,
     WmiVersion(1)] uint32 TargetPortalGroupTag;

    [read,
     WmiDataId(3),
     DisplayName("Number of elements in RedirectPortalList array") : amended,
     cpp_quote("\n    // Number of elements in RedirectPortalList array\n"),
     Description("Number of elements in RedirectPortalList array") : amended,
     WmiVersion(1)
    ] uint32 ConnectionCount;

    [read,
     WmiDataId(4),
     DisplayName("Redirect Portal info for each connection") : amended,
     Description("Redirect portal info - one element for each connection in the session") : amended,
     WmiSizeIs("ConnectionCount"),
     WmiVersion(1)
    ] ISCSI_RedirectPortalInfo RedirectPortalList[];
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_RedirectSessionInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_iscsi_redirectsessioninfo)データ構造体。

 

 





