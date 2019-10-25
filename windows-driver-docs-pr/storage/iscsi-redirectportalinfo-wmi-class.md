---
title: ISCSI\_RedirectPortalInfo WMI クラス
description: ISCSI\_RedirectPortalInfo WMI クラス
ms.assetid: 55730446-7c8b-4c9d-9473-f9bb6edd603e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 143aaec79e33f9687bf14db4ce07c2c65fd328ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845382"
---
# <a name="iscsi_redirectportalinfo-wmi-class"></a>ISCSI\_RedirectPortalInfo WMI クラス


ISCSI\_RedirectPortalInfo WMI クラスには、iSCSI ポータルのコレクションに関する情報が含まれています。 このクラスは、*管理 .mof*で次のように定義されています。

```cpp
class ISCSI_RedirectPortalInfo
{
    [read,
     WmiDataId(1),
     Description("A uniquely generated connection ID. Do not confuse this with CID."): amended,
     WmiVersion(1)
     ] uint64 UniqueConnectionId;

    [read,
     WmiDataId(2),
     Description("Original Target IP Address given in the login"): amended,
     WmiVersion(1)] ISCSI_IP_Address OriginalIPAddr;

    [read,
     WmiDataId(3),
     Description("Original Target portal's socket number given in the login"): amended,
     WmiVersion(1)] uint32 OriginalPort;

    [read,
     WmiDataId(4),
     Description("Redirected Target IP Address"): amended,
     WmiVersion(1)] ISCSI_IP_Address RedirectedIPAddr;

    [read,
     WmiDataId(5),
     Description("Redirected Target portal's socket number"): amended,
     WmiVersion(1)] uint32 RedirectedPort;

    [read,
     WmiDataId(6),
     Description("TRUE if login was redirected. RedirectedIPAddr and RedirectedPort are valid then."): amended,
     WmiVersion(1)] uint8 Redirected;

    [read,
     WmiDataId(7),
     Description("TRUE if the redirection is temporary. FALSE otherwise"): amended,
     WmiVersion(1)] uint8 TemporaryRedirect;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**ISCSI\_RedirectPortalInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_redirectportalinfo)データ構造を生成します。

 

 





