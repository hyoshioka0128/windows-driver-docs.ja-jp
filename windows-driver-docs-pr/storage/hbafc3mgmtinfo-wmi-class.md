---
title: HBAFC3MgmtInfo WMI クラス
description: HBAFC3MgmtInfo WMI クラス
ms.assetid: 7c3e5b7e-aed9-4d82-91d9-e0c7b8f5ddf6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5cb54755cc1cfaa8b170fd5f8be4b28951dfee71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386184"
---
# <a name="hbafc3mgmtinfo-wmi-class"></a>HBAFC3MgmtInfo WMI クラス


## <span id="ddk_hbafc3mgmtinfo_wmi_class_kr"></span><span id="DDK_HBAFC3MGMTINFO_WMI_CLASS_KR"></span>


WMI クライアントでは、HBAFC3MgmtInfo クラスを使用して、クエリ、HBA のミニポート ドライバー FC3 管理については、ファイバー チャネル アダプターに関連付けられています。 FC3 はファイバー チャネル プロトコルの一般的なサービス層を表します。 ノードの複数のポート間に共通するサービスのセットを定義します。 一般的なサービス層の詳細については、T11 委員会を参照してください。*ファイバー チャネル HBA API*仕様。

HBAFC3MgmtInfo クラスは次のように定義されている*Hbaapi.mof*:

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

WMI ツール スイートによってコンパイルされると、このクラスの定義を生成、 [ **HBAFC3MgmtInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





