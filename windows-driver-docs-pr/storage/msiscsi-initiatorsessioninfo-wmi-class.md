---
title: MSiSCSI\_InitiatorSessionInfo WMI クラス
description: MSiSCSI\_InitiatorSessionInfo WMI クラス
ms.assetid: 73053af8-80b0-4cab-8e27-c651be8f0e8c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1d591b06defb69b6ddd5634ca6bb64a2e3462113
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845352"
---
# <a name="msiscsi_initiatorsessioninfo-wmi-class"></a>MSiSCSI\_InitiatorSessionInfo WMI クラス


## <span id="ddk_msiscsi_initiatorsessioninfo_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORSESSIONINFO_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorSessionInfo WMI クラスは、指定された HBA イニシエーターに属するセッションとコレクションに関連付けられている情報を公開します。

このクラスは記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用してクラスを登録する必要があります。

MSiSCSI\_InitiatorSessionInfo クラスは、*管理 .mof*で定義されています。

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

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_InitiatorSessionInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_initiatorsessioninfo)データ構造体を生成します。

 

 





