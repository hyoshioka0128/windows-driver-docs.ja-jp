---
title: MSiSCSI\_SecurityCapabilities WMI クラス
description: MSiSCSI\_SecurityCapabilities WMI クラス
ms.assetid: 50f7aa98-0743-4775-808b-c5a90dc1d0fe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f4a6400fbfaf426119ae5d18702825e8d464fbac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845327"
---
# <a name="msiscsi_securitycapabilities-wmi-class"></a>MSiSCSI\_SecurityCapabilities WMI クラス


## <span id="ddk_msiscsi_securitycapabilities_wmi_class_kr"></span><span id="DDK_MSISCSI_SECURITYCAPABILITIES_WMI_CLASS_KR"></span>


MSiSCSI\_SecurityCapabilities WMI クラスは、イニシエーターのセキュリティ機能を記述します。

It が管理する HBA が IPsec をサポートしている場合、ミニポートドライバーは MSiSCSI\_SecurityCapabilities クラスを実装する必要があります。

MSiSCSI\_SecurityCapabilities クラスは記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが持つ特定の物理デバイスオブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。管理.

MSiSCSI\_SecurityCapabilities クラスは、*構成 .mof*で定義されています。

```cpp
class MSiSCSI_SecurityCapabilities {
  [key] string  InstanceName;
  boolean  Active;
  [read, DisplayName("Protect iSCSI") : amended, 
    WmiDataId(1), description("TRUE if the HBA can use IPsec 
    to protect iSCSI traffic") : amended]
    boolean  ProtectiScsiTraffic;
  [read, WmiDataId(2), DisplayName("Protect iSNS") : 
    amended, description("TRUE if the HBA can use IPsec to 
    protect iSNS traffic") : amended] 
    boolean  ProtectiSNSTraffic;
  [read, WmiDataId(3), DisplayName("Certificates Supported") 
    : amended, description("TRUE if HBA supports 
    certificates") : amended] 
    boolean  CertificatesSupported;
  [read, WmiDataId(4), DisplayName("Encryption Types 
    Available") : amended, description("Count of encryption 
    types available")] 
    uint32  EncryptionAvailableCount;
  [read, WmiDataId(5), 
    WmiSizeIs("EncryptionAvailableCount"), 
    ENCRYPTION_TYPES_QUALIFIERS, DisplayName("Encryption 
    Types") : amended] 
    uint32  EncryptionAvailable[];
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_SecurityCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_securitycapabilities)データ構造を生成します。

 

 





