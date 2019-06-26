---
title: ISCSI\_RedirectPortalInfo WMI クラス
description: ISCSI\_RedirectPortalInfo WMI クラス
ms.assetid: 55730446-7c8b-4c9d-9473-f9bb6edd603e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: edfb8ac11203552a8d32f5e924c7be5683f35718
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378414"
---
# <a name="iscsiredirectportalinfo-wmi-class"></a>ISCSI\_RedirectPortalInfo WMI クラス


ISCSI\_RedirectPortalInfo WMI クラスには、iSCSI ポータルのコレクションに関する情報が含まれています。 このクラスが次のように定義されている*Mgmt.mof*します。

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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_RedirectPortalInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_iscsi_redirectportalinfo)データ構造体。

 

 





