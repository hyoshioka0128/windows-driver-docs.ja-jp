---
title: MSiSCSI\_RADIUSConfig WMI クラス
description: MSiSCSI\_RADIUSConfig WMI クラス
ms.assetid: e0fd1fea-3d8c-4d25-a9fd-0e115ecb8163
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a13d03ea3fd135742721563b5f16bdd33df42cf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580803"
---
# <a name="msiscsiradiusconfig-wmi-class"></a>MSiSCSI\_RADIUSConfig WMI クラス


## <span id="ddk_msiscsi_radiusconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_RADIUSCONFIG_WMI_CLASS_KR"></span>


MSiSCSI\_RADIUSConfig WMI クラスは、イニシエーターが、リモート認証ダイヤルイン ユーザー サービス (RADIUS) を使用して、発信側サービスを使用する必要がある情報を提供するかどうかを示します。

イニシエーターは、チャレンジ ハンドシェイク認証プロトコル (CHAP) のチャレンジ ハンドシェイク中に認証を実行するのに RADIUS サーバーを使用します。

ミニポート ドライバーは、MSiSCSI を実装する必要があります\_RADIUSConfig クラス RADIUS CHAP 認証を使用して、管理する HBA がサポートしている場合。

CHAP 資格情報の一元管理できるため、可能であれば、RADIUS を使用してください。

MSiSCSI\_RADIUSConfig WMI クラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付け、ミニポート ドライバーは、特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要がありますミニポート ドライバー管理します。

MSiSCSI\_RADIUSConfig クラスで定義されます*Config.mof*します。

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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_RADIUSConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff563112)データ構造体。

 

 





