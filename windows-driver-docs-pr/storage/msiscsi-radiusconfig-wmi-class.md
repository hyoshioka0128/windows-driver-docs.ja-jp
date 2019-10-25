---
title: MSiSCSI\_RADIUSConfig WMI クラス
description: MSiSCSI\_RADIUSConfig WMI クラス
ms.assetid: e0fd1fea-3d8c-4d25-a9fd-0e115ecb8163
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5e1e2175576e2a0af894b77716e391d96cb328bc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845331"
---
# <a name="msiscsi_radiusconfig-wmi-class"></a>MSiSCSI\_RADIUSConfig WMI クラス


## <span id="ddk_msiscsi_radiusconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_RADIUSCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_RADIUSConfig WMI クラスは、イニシエーターがリモート認証ダイヤルインユーザーサービス (RADIUS) を使用し、イニシエーターがサービスを使用するために必要な情報を提供するかどうかを示します。

イニシエーターは RADIUS サーバーを使用して、チャレンジハンドシェイク認証プロトコル (CHAP) のチャレンジハンドシェイク中に認証を実行します。

管理する HBA が CHAP 認証に RADIUS を使用してサポートする場合、ミニポートドライバーは MSiSCSI\_RADIUSConfig クラスを実装する必要があります。

可能な限り RADIUS を使用することをお勧めします。これにより、CHAP 資格情報を一元的に管理できます。

MSiSCSI\_RADIUSConfig WMI クラスは、記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用してクラスを登録する必要があります。

MSiSCSI\_RADIUSConfig クラスは、*構成 .mof*で定義されています。

```cpp
class MSiSCSI_RADIUSConfig {
  [key] string  InstanceName;
  boolean  Active;
  [WmiDataId(1), read, write, description("HBA should use 
    RADIUS for CHAP authentication") : amended] 
    boolean  UseRADIUSForCHAP;
  [WmiDataId(2), read, write, description("Size in bytes of 
    shared secret for RADIUS servers") : amended] 
    uint32  SharedSecretSizeInBytes;
  [WmiDataId(3), read, write, description("Fixed Addresses 
    of RADIUS server") : amended] 
    ISCSI_IP_Address  RADIUSServer;
  [WmiDataId(4), read, write, description("Fixed Addresses 
    of backup RADIUS server") : amended] 
    ISCSI_IP_Address  BackupRADIUSServer;
  [WmiDataId(5), read, write, 
    WmiSizeIs("SharedSecretSizeInBytes"), 
    description("Shared secret for RADIUS servers") :
    amended] 
    uint8 SharedSecret[];
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_RADIUSConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsicfg/ns-iscsicfg-_msiscsi_radiusconfig)データ構造体を生成します。

 

 





