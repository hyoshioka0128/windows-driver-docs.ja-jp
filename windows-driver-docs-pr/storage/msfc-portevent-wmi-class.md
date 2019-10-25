---
title: MSFC\_PortEvent WMI クラス
description: MSFC\_PortEvent WMI クラス
ms.assetid: 38b8e358-b118-4a0c-ac47-2f257d0ed1bf
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d4a1229c1e7accc503aeb13cf5e366a6fdcc529e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845605"
---
# <a name="msfc_portevent-wmi-class"></a>MSFC\_PortEvent WMI クラス


## <span id="ddk_msfc_portevent_wmi_class_kr"></span><span id="DDK_MSFC_PORTEVENT_WMI_CLASS_KR"></span>


WMI プロバイダーは、MSFC\_PortEvent WMI クラスを使用してポートイベントを報告します。

MSFC\_PortEvent クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class MSFC_PortEvent : WMIEvent {
  [key] 
  string InstanceName;
  boolean Active;
  [WmiDataId(1), Description("Type of event") : amended,
    EVENT_TYPES_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Fabric port id") : amended]
    uint32 FabricPortId;
  [WmiDataId(3), Description("Port WWN") : amended,
    HBAType("HBA_WWN")] uint8  PortWWN[8];
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**MSFC\_PortEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_portevent)

 

 





