---
title: MSFC\_HBAPortAttributesResults WMI クラス
description: MSFC\_HBAPortAttributesResults WMI クラス
ms.assetid: f268a653-e3ee-47d0-9af8-925dc0545a2b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b8bbffa9a20953faec31d77bed0cef2f25bf2cb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376752"
---
# <a name="msfchbaportattributesresults-wmi-class"></a>MSFC\_HBAPortAttributesResults WMI クラス


## <span id="ddk_msfc_hbaportattributesresults_wmi_class_kr"></span><span id="DDK_MSFC_HBAPORTATTRIBUTESRESULTS_WMI_CLASS_KR"></span>


WMI クライアントが使用、MSFC\_HBAPortAttributesResults WMI クラスの hba ポートの属性の HBA ミニポート ドライバーを照会します。

MSFC\_HBAPortAttributesResults クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_HBAPortAttributesResults {
    [HBAType("HBA_WWN"), WmiDataId(1) ] uint8  NodeWWN[8];
    [HBAType("HBA_WWN"), WmiDataId(2) ] uint8  PortWWN[8];
    [ WmiDataId(3) ] uint32 PortFcId;
    [HBAType("HBA_PORTTYPE"), Values{"Unknown", "Other",
      "Not present", "Fabric", "Public Loop",
      "HBA_PORTTYPE_FLPORT", "Fabric Port",
      "Fabric expansion port", "Generic Fabric Port",
      "Private Loop", "Point to Point"} : amended,
      ValueMap{"1", "2", "3", "5", "6", "7", "8", "9",
      "10", "20", "21"},
      WmiDataId(4) ] uint32  PortType;
    [HBAType("HBA_PORTSTATE"), Values{"Unknown", "Operational",
      "User Offline", 
      "Bypassed", "In diagnostics mode", "Link Down", 
      "Port Error", "Loopback"} : amended,
      ValueMap{"1","2","3","4","5","6","7","8"},
      WmiDataId(5) ] uint32  PortState;
    [HBAType("HBA_COS"), WmiDataId(6) ] 
      uint32 PortSupportedClassofService;
   [HBAType("HBA_FC4TYPES"), WmiDataId(7)] 
      uint8 PortSupportedFc4Types[32];
    [HBAType("HBA_FC4TYPES"), WmiDataId(8)]
      uint8 PortActiveFc4Types[32];
    [HBAType("HBA_PORTSPEED"),
      Values{"1 GBit/sec", "2 GBit/sec", "10 GBit/sec", 
      "4 GBit/sec"} : amended,
      ValueMap{"1", "2", "4", "8"},
      WmiDataId(9)] uint32  PortSupportedSpeed;
    [HBAType("HBA_PORTSPEED"),
      Values{"1 GBit/sec", "2 GBit/sec", 
      "10 GBit/sec", "4 GBit/sec"} : amended,
      ValueMap{"1", "2", "4", "8"},
      WmiDataId(10) ] uint32  PortSpeed;
    [WmiDataId(11) ] uint32  PortMaxFrameSize;
    [HBAType("HBA_WWN"), WmiDataId(12) ] uint8  FabricName[8];
    [ WmiDataId(13) ] uint32  NumberofDiscoveredPorts;
};
```

このクラスをコンパイル時に定義には、次のデータ構造が生成されます。

[**MSFC\_HBAPortAttributesResults**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)

この WMI クラスに関連付けられているメソッドはありません。

 

 





