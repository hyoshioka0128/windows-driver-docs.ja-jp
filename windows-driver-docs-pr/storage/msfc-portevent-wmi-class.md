---
title: MSFC\_PortEvent WMI クラス
description: MSFC\_PortEvent WMI クラス
ms.assetid: 38b8e358-b118-4a0c-ac47-2f257d0ed1bf
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a954b65264cf0f08b6835615cecde9a3fc5fa840
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386574"
---
# <a name="msfcportevent-wmi-class"></a>MSFC\_PortEvent WMI クラス


## <span id="ddk_msfc_portevent_wmi_class_kr"></span><span id="DDK_MSFC_PORTEVENT_WMI_CLASS_KR"></span>


WMI プロバイダーでは、MSFC\_PortEvent WMI クラス ポート イベントを報告します。

MSFC\_PortEvent クラスが次のように定義されている*Hbaapi.mof*:

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

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_PortEvent**](https://msdn.microsoft.com/library/windows/hardware/ff562516)

 

 





