---
title: HBAFC3MgmtInfo WMI クラス
description: HBAFC3MgmtInfo WMI クラス
ms.assetid: 7c3e5b7e-aed9-4d82-91d9-e0c7b8f5ddf6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 958e34d72cfa4501960f356b9f094c6d3162100c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845235"
---
# <a name="hbafc3mgmtinfo-wmi-class"></a>HBAFC3MgmtInfo WMI クラス


## <span id="ddk_hbafc3mgmtinfo_wmi_class_kr"></span><span id="DDK_HBAFC3MGMTINFO_WMI_CLASS_KR"></span>


WMI クライアントは、HBAFC3MgmtInfo クラスを使用して、ファイバーチャネルアダプターに関連付けられている FC3 管理情報の HBA ミニポートドライバーを照会します。 FC3 は、ファイバーチャネルプロトコルの共通サービス層を参照します。 ノードの複数のポートに共通する一連のサービスを定義します。 共通サービスレイヤーの詳細については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。

HBAFC3MgmtInfo クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class HBAFC3MgmtInfo {
  [Description ("Unique identifier for the adapter. This"
    "identifier must be unique among all adapters. "
    "The same value for the identifier must be used "
    "for the same adapter in other classes that expose "
    "adapter information") : amended,
   WmiRefClass("MSFC_FibreChannelAdapter"),
   WmiRefProperty("UniqueAdapterId"), WmiDataId(1) 
     uint64  UniqueAdapterId;
// CIM_FibreChannelAdapter REF
  [HBAType("HBA_WWN"), WmiDataId(2)] uint8  wwn[8];
  [WmiDataId(3)] uint32  unittype;
  [WmiDataId(4)] uint32  PortId;
  [WmiDataId(5)] uint32  NumberOfAttachedNodes;
  [WmiDataId(6)] uint16  IPVersion;
  [WmiDataId(7)] uint16  UDPPort;
  [WmiDataId(8)] uint8  IPAddress[16];
  [WmiDataId(9)] uint16 reserved;
  [WmiDataId(10)] uint16  TopologyDiscoveryFlags;
  [WmiDataId(11)] uint32  reserved1;
};
```

このクラス定義は、WMI ツールスイートによってコンパイルされると、 [**HBAFC3MgmtInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)データ構造体を生成します。 この WMI クラスに関連付けられているメソッドはありません。

 

 





