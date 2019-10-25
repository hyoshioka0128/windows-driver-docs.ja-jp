---
title: MSiSCSI\_InitiatorNodeFailureEvent WMI クラス
description: MSiSCSI\_InitiatorNodeFailureEvent WMI クラス
ms.assetid: 2e542667-4da8-447b-b625-2cd27d52da61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 041bb46383fd593891cf8963210e82015166a61b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845353"
---
# <a name="msiscsi_initiatornodefailureevent-wmi-class"></a>MSiSCSI\_InitiatorNodeFailureEvent WMI クラス


## <span id="ddk_msiscsi_initiatornodefailureevent_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORNODEFAILUREEVENT_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorNodeFailureEvent WMI クラスは、ノード障害が発生したときにイベントを発生させます。

このクラスは記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用してクラスを登録する必要があります。

MSiSCSI\_InitiatorNodeFailureEvent WMI クラスは、ノード障害が発生したときにイベントを発生させます。 このクラスは、*管理 .mof*で定義されています。

```cpp
class MSiSCSI_InitiatorNodeFailureEvent : WMIEvent {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [read, WmiDataId(1), WmiTimeStamp, WmiVersion(1)] 
    uint64  FailureTime;
  [read, WmiDataId(2),
    ISCSI_INITIATOR_FAILURE_TYPE_QUALIFIERS, WmiVersion(1)] 
    ISCSI_INITIATOR_FAILURE_TYPE  FailureType;
  [read, WmiDataId(3), WmiVersion(1),
    MaxLen(MAX_ISCSI_NAME_LEN)] 
    string  TargetFailureName;
  [read, WmiDataId(4), WmiVersion(1)] 
  ISCSI_IP_Address  TargetFailureAddr;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_InitiatorNodeFailureEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_initiatornodefailureevent)データ構造体を生成します。

 

 





