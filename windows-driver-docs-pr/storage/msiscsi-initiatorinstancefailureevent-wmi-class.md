---
title: MSiSCSI\_InitiatorInstanceFailureEvent WMI クラス
description: MSiSCSI\_InitiatorInstanceFailureEvent WMI クラス
ms.assetid: 58ddfaf7-d2ec-4b06-8eef-f7b07285963d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1d50afa102299a7a928be302acb7da5646211460
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384333"
---
# <a name="msiscsiinitiatorinstancefailureevent-wmi-class"></a>MSiSCSI\_InitiatorInstanceFailureEvent WMI クラス


## <span id="ddk_msiscsi_initiatorinstancefailureevent_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORINSTANCEFAILUREEVENT_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorInstanceFailureEvent WMI クラスは、発信側インスタンスのエラーが発生したときにイベントを発生させます。

このクラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付けられているため、ミニポート ドライバーは、ミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。

MSiSCSI\_InitiatorInstanceFailureEvent クラスで定義されます*Mgmt.mof*します。

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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_InitiatorInstanceFailureEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_msiscsi_initiatorinstancefailureevent)データ構造体。

 

 





