---
title: MSiSCSI\_NICConfig WMI クラス
description: MSiSCSI\_NICConfig WMI クラス
ms.assetid: 9b7a466d-a9bb-41c5-8f38-e5baf21e863a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1893b7a4731cf1d84325acf3db56149b8dcf841d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845342"
---
# <a name="msiscsi_nicconfig-wmi-class"></a>MSiSCSI\_NICConfig WMI クラス


## <span id="ddk_msiscsi_nicconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_NICCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_NICConfig WMI クラスは、ネットワークインターフェイスカード (NIC) ポートを記述します。

HBA イニシエーターのミニポートドライバーは、HBA の各ポートに対して、MSiSCSI\_NICConfig クラスのインスタンスを1つ作成する必要があります。

MSiSCSI\_NICConfig クラスは、*構成 .mof*で定義されています。

```cpp
class MSiSCSI_NICConfig {
  [key] string  InstanceName;
  boolean  Active;
  [read, WmiDataId(1), DisplayName("Link Speed") : amended, 
    Description("Speed of network link in megabits per 
    second") : amended] 
    uint32  LinkSpeed;
  [read, WmiDataId(2), DisplayName("Max Link Speed") : 
    amended, Description("Maximum Speed of network link in 
    megabits per second") : amended] 
    uint32  MaxLinkSpeed;
  [read, WmiDataId(3), DisplayName("Link State") : amended, 
    description("Link State") : amended, 
    Values{"Media Disconnected", "Media Connected"} : 
    amended,
    ValueMap{"0", "1"}] 
    uint32  LinkState;
  [read, WmiDataId(4), DisplayName("Max Frame Size") : 
    amended, description("Maximum frame size") : amended] 
    uint32  MaxFrameSize;
  [read, WmiDataId(5), DisplayName("MAC Address") : amended, 
    description("Ethernet MAC Address") : amended] 
    uint8  MacAddress[6];
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_NICConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_nicconfig)データ構造体を生成します。

 

 





