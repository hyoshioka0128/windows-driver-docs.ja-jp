---
title: ISCSI\_RedirectSessionInfo WMI クラス
description: ISCSI\_RedirectSessionInfo WMI クラス
ms.assetid: eb1ec866-2dcd-4099-a24f-ae1d0c702b95
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cda9df1cb43db76a03016c39fa4a2ffe820087a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823689"
---
# <a name="iscsi_redirectsessioninfo-wmi-class"></a>ISCSI\_RedirectSessionInfo WMI クラス


ISCSI\_RedirectSessionInfo WMI クラスには、iSCSI セッションの接続のコレクションが含まれています。 このクラスは、管理 .mof で次のように定義されてい*ます。*

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

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**ISCSI\_RedirectSessionInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_redirectsessioninfo)データ構造を生成します。

 

 





