---
title: MSiSCSI\_SecurityCapabilities WMI クラス
description: MSiSCSI\_SecurityCapabilities WMI クラス
ms.assetid: 50f7aa98-0743-4775-808b-c5a90dc1d0fe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2e6f7a3932ada476e569ca7736cffeef408462f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384667"
---
# <a name="msiscsisecuritycapabilities-wmi-class"></a>MSiSCSI\_SecurityCapabilities WMI クラス


## <span id="ddk_msiscsi_securitycapabilities_wmi_class_kr"></span><span id="DDK_MSISCSI_SECURITYCAPABILITIES_WMI_CLASS_KR"></span>


MSiSCSI\_SecurityCapabilities WMI クラスが、開始側のセキュリティ機能について説明します。

ミニポート ドライバーは、MSiSCSI を実装する必要があります\_SecurityCapabilities クラスを管理する HBA が IPsec をサポートしている場合。

MSiSCSI\_SecurityCapabilities クラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付け、ミニポート ドライバーは、特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要がありますミニポートドライバーを管理します。

MSiSCSI\_SecurityCapabilities クラスで定義されます*Config.mof*します。

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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_SecurityCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsicfg/ns-iscsicfg-_msiscsi_securitycapabilities)データ構造体。

 

 





