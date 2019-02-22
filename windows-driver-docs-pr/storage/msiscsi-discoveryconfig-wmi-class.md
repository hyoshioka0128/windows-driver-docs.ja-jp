---
title: MSiSCSI\_DiscoveryConfig WMI クラス
description: MSiSCSI\_DiscoveryConfig WMI クラス
ms.assetid: dbf170ba-92ab-47bd-a076-5f54129305a5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a9849b12b0f6254d69d9ded7c8eafdc91635f296
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559438"
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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_DiscoveryConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff562991)データ構造体。

 

 





