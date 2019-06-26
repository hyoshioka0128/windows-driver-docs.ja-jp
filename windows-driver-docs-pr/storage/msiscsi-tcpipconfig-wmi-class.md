---
title: MSiSCSI\_TCPIPConfig WMI クラス
description: MSiSCSI\_TCPIPConfig WMI クラス
ms.assetid: 57451576-a900-4eaa-b229-bda79a81d014
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49bed145c38b6cb358ee1427183883adcf499e3d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384663"
---
# <a name="msiscsitcpipconfig-wmi-class"></a>MSiSCSI\_TCPIPConfig WMI クラス


## <span id="ddk_msiscsi_tcpipconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_TCPIPCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_TCPIPConfig WMI クラスは、HBA の IP アドレスのいずれかの TCP/IP 構成情報を報告します。

アダプターのミニポート ドライバーでは、アダプターがサポートされる各 IP アドレスに対して、このクラスの 1 つのインスタンスを作成する必要があります。

MSiSCSI\_TCPIPConfig クラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付け、ミニポート ドライバーは、ミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。

MSiSCSI\_TCPIPConfig クラスで定義されます*Config.mof*します。

```cpp
class MSiSCSI_TCPIPConfig {
  [key] string  InstanceName;
  boolean  Active;
  [read, write, WmiDataId(1), DisplayName("Use Link Local 
    Address") : amended, description("TRUE if the HBA should 
    use a link local address as its ip address") : amended] 
    boolean  UseLinkLocalAddress;
  [read, write, WmiDataId(2), displayName("DHCP Enabled") : 
    amended, description("TRUE if the HBA should use DHCP") 
    : amended] 
    boolean  EnableDHCP;
  [read, WmiDataId(3), description("IP Versions supported") 
    : amended, 
    BitValues{ "IPV4", "IPV6"},
    BitMap{"0x00000001", "0x00000002"}] 
    uint32  IPVersions;
  [read, write, WmiDataId(4), DisplayName("Static IP 
    Address") : amended, description("Static IP address for 
    the HBA") : amended]
    ISCSI_IP_Address  StaticIpAddress;
  [read, write, WmiDataId(5), DisplayName("Default Gateway") 
    : amended, Description("Static Default Gateway IP 
    address") : amended]
    ISCSI_IP_Address  DefaultGateway;
  [read, write, WmiDataId(6), DisplayName("Subnet Mask") : 
    amended, Description("Static Subnet Mask") : amended] 
    ISCSI_IP_Address  SubnetMask;
  [read, write, WmiDataId(7), DisplayName("Preferred DNS 
    Server") : amended, Description("Preferred DNS Server") 
    : amended] 
    ISCSI_IP_Address  PreferredDNSServer;
  [read, write, WmiDataId(8), DisplayName("Alternate DNS 
    Server") : amended, Description("Alternate DNS Server") 
    : amended] 
    ISCSI_IP_Address  AlternateDNSServer;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_TCPIPConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsicfg/ns-iscsicfg-_msiscsi_tcpipconfig)データ構造体。

 

 





