---
title: MSiSCSI\_InitiatorInstanceFailureEvent WMI クラス
description: MSiSCSI\_InitiatorInstanceFailureEvent WMI クラス
ms.assetid: 58ddfaf7-d2ec-4b06-8eef-f7b07285963d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6db66e08b4f80e2f078b95f4f97025670bf7f102
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845359"
---
# <a name="msiscsi_initiatorinstancefailureevent-wmi-class"></a>MSiSCSI\_InitiatorInstanceFailureEvent WMI クラス


## <span id="ddk_msiscsi_initiatorinstancefailureevent_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORINSTANCEFAILUREEVENT_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorInstanceFailureEvent WMI クラスは、イニシエーターインスタンスの障害が発生したときにイベントを発生させます。

このクラスは記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用してクラスを登録する必要があります。

MSiSCSI\_InitiatorInstanceFailureEvent クラスは、*管理 .mof*で定義されています。

```cpp
class MSiSCSI_InitiatorInstanceFailureEvent : WMIEvent {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [read, WmiDataId(1),
    ISCSI_INITIATOR_NODE_FAILURE_TYPE_QUALIFIERS, 
    WmiVersion(1)] 
    ISCSI_INITIATOR_NODE_FAILURE_TYPE  FailureType;
  [read, WmiDataId(2), WmiVersion(1),
    MaxLen(MAX_ISCSI_NAME_LEN)] 
    string  RemoteNodeName;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_InitiatorInstanceFailureEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_initiatorinstancefailureevent)データ構造体を生成します。

 

 





