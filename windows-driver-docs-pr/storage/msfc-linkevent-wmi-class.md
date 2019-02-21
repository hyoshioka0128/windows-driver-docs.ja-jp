---
title: MSFC\_LinkEvent WMI クラス
description: MSFC\_LinkEvent WMI クラス
ms.assetid: 9507fb1a-ce2a-4ce9-8272-77c8c9d0a92c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5428809627f1e8a7559a192d9bf060fefea84fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559435"
---
# <a name="msfclinkevent-wmi-class"></a>MSFC\_LinkEvent WMI クラス


## <span id="ddk_msfc_linkevent_wmi_class_kr"></span><span id="DDK_MSFC_LINKEVENT_WMI_CLASS_KR"></span>


WMI プロバイダーでは、MSFC\_LinkEvent WMI クラスは、リンクのイベントを報告します。

MSFC\_LinkEvent クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MSFC_LinkEvent : WMIEvent {
  [key] 
  string InstanceName;
  boolean Active;
  [WmiDataId(1), Description("Type of event") : amended,
    EVENT_TYPES_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Discovered Port WWN") : amended,    HBAType("HBA_WWN")]uint8  AdapterWWN[8];
  [WmiDataId(3), Description("Size of RLIR buffer") : amended]
    uint32 RLIRBufferSize;
  [WmiDataId(4), Description("Size of RLIR buffer") : amended,
     WmiSizeIs("RLIRBufferSize")]uint8 RLIRBuffer[];
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**MSFC\_LinkEvent**](https://msdn.microsoft.com/library/windows/hardware/ff562514)

この WMI クラスに関連付けられているメソッドはありません。

 

 





