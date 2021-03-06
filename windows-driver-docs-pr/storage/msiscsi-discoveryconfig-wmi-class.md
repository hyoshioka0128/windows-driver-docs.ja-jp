---
title: MSiSCSI\_DiscoveryConfig WMI クラス
description: MSiSCSI\_DiscoveryConfig WMI クラス
ms.assetid: dbf170ba-92ab-47bd-a076-5f54129305a5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 99d1578588bc237f011ec94abb949db76a0e7000
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379700"
---
# <a name="msiscsidiscoveryconfig-wmi-class"></a>MSiSCSI\_DiscoveryConfig WMI クラス


## <span id="ddk_msiscsi_discoveryconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_DISCOVERYCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_DiscoveryConfig WMI クラスは、イニシエーターが探索の実行に使用する方法を報告します。

このクラスが次のように定義されている*Config.mof*します。

```cpp
class MSiSCSI_DiscoveryConfig {
  [key] string  InstanceName;
  boolean  Active;
  [WmiDataId(1), read, write, description("HBA should
    perform target discovery via iSNS") : amended] 
    boolean  PerformiSNSDiscovery;
  [WmiDataId(2), read, write, description("HBA should 
    perform target discovery via SLP") : amended] 
    boolean  PerformSLPDiscovery;
  [WmiDataId(3), read, write, description("Automatic 
    discovery of iSNS server") : amended] 
    boolean  AutomaticiSNSDiscovery;
  [WmiDataId(4), read, write, MaxLen(256), 
    description("Default initiator name for registering with 
    iSNS") : amended] 
    string  InitiatorName;
  [WmiDataId(5), read, write, description("Fixed Addresses 
    of iSNS servers") : amended] 
    ISCSI_IP_Address  iSNSServer;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_DiscoveryConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsicfg/ns-iscsicfg-_msiscsi_discoveryconfig)データ構造体。

 

 





