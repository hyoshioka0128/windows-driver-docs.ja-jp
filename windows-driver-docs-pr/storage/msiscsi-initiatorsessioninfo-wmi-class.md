---
title: MSiSCSI\_InitiatorSessionInfo WMI クラス
description: MSiSCSI\_InitiatorSessionInfo WMI クラス
ms.assetid: 73053af8-80b0-4cab-8e27-c651be8f0e8c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 44a2e52a194b57d50885f2ba20f15f54af2e7ce5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370430"
---
# <a name="msiscsiinitiatorsessioninfo-wmi-class"></a>MSiSCSI\_InitiatorSessionInfo WMI クラス


## <span id="ddk_msiscsi_initiatorsessioninfo_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORSESSIONINFO_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorSessionInfo WMI クラスは、セッションと、指定された HBA イニシエーターに属しているコレクションに関連付けられている情報を公開します。

このクラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付けられているため、ミニポート ドライバーは、ミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。

MSiSCSI\_InitiatorSessionInfo クラスで定義されます*Mgmt.mof*します。

```cpp
class MSiSCSI_InitiatorSessionInfo {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [WmiDataId(1), DisplayName("Adapter Id") : amended, 
    DisplayInHex, description("Id that is globally unique to
    each instance of each adapter. Using the address of the 
    Adapter Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(2), read, DisplayName("Count of Elements in 
    SessionsList array") : amended,
    cpp_quote(
    "\n    // Number of elements in SessionList array\n"),
    Description("Number of elements in SessionList array") : 
    amended] 
    uint32  SessionCount;
  [WmiDataId(3), read, DisplayName("List Of Sessions") :
    amended, Description("Variable length array of sessions.
    SessionCount specifies the number of elements in the 
    array") : amended, WmiSizeIs("SessionCount")]  
    ISCSI_SessionStaticInfo  SessionsList[];
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_InitiatorSessionInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_msiscsi_initiatorsessioninfo)データ構造体。

 

 





