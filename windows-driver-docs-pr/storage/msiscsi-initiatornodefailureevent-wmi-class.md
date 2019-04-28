---
title: MSiSCSI\_InitiatorNodeFailureEvent WMI クラス
description: MSiSCSI\_InitiatorNodeFailureEvent WMI クラス
ms.assetid: 2e542667-4da8-447b-b625-2cd27d52da61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 66639c294f1eaf5b7b055c9496ce909eea4dd435
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382529"
---
# <a name="msiscsiinitiatornodefailureevent-wmi-class"></a>MSiSCSI\_InitiatorNodeFailureEvent WMI クラス


## <span id="ddk_msiscsi_initiatornodefailureevent_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORNODEFAILUREEVENT_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorNodeFailureEvent WMI クラスは、ノード障害が発生したときにイベントを発生させます。

このクラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付けられているため、ミニポート ドライバーは、ミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。

MSiSCSI\_InitiatorNodeFailureEvent WMI クラスは、ノード障害が発生したときにイベントを発生させます。 このクラスで定義されます*Mgmt.mof*します。

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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_InitiatorNodeFailureEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563046)データ構造体。

 

 





