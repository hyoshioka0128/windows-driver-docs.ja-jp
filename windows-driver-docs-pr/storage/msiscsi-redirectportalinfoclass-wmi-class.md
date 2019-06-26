---
title: MSiSCSI\_RedirectPortalInfoClass WMI クラス
description: MSiSCSI\_RedirectPortalInfoClass WMI クラス
ms.assetid: 38f510ed-1f31-4b3c-84c6-515f5d42a1f8
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c73e80c50602a1a242fd51089057b516b878686e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384675"
---
# <a name="msiscsiredirectportalinfoclass-wmi-class"></a>MSiSCSI\_RedirectPortalInfoClass WMI クラス


MSiSCSI\_RedirectPortalInfoClass WMI クラスには、アダプタ ID のセッションのコレクションが含まれています さらに、各セッションのポータルのリダイレクトの情報が含まれています。 このクラスが次のように定義されている*Mgmt.mof します。*

```cpp
class MSiSCSI_RedirectPortalInfoClass
{
    [read,key] String InstanceName;

    [read] boolean Active;

    [read,
     WmiDataId(1),
     DisplayName("Adapter Id") : amended,
     DisplayInHex,
     description("Id that is globally unique for all instances of iSCSI initiators.") : amended,
     WmiVersion(1)
    ]
    uint64 UniqueAdapterId;

    [read,
     WmiDataId(2),
     DisplayName("Number of session on the adapter : Number of elements in RedirectSessionInfo array") : amended,
     Description("Number of elements in RedirectSessionInfo array") : amended,
     WmiVersion(1)
    ] uint32 SessionCount;

    [read,
     WmiDataId(3),
     DisplayName("List Of ISCSI_RedirectSessionInfo ") : amended,
     Description("Variable length array of ISCSI_RedirectSessionInfo. SessionCount specifies the number of elements in the array. NOTE: this is a variable length array.") : amended,
     WmiSizeIs("SessionCount"),
     WmiVersion(1)
    ] ISCSI_RedirectSessionInfo RedirectSessionList[];
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_RedirectPortalInfoClass** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_msiscsi_redirectportalinfoclass)データ構造体。

 

 





