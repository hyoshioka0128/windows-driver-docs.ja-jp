---
title: MSiSCSI\_NICPerformance WMI クラス
description: MSiSCSI\_NICPerformance WMI クラス
ms.assetid: e5894b20-8ea7-46ec-9960-3d9891b06ac4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9eb630d3ae93d32e7695ab5bdc65d5df0735b324
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580760"
---
# <a name="msiscsinicperformance-wmi-class"></a>MSiSCSI\_NICPerformance WMI クラス


## <span id="ddk_msiscsi_nicperformance_wmi_class_kr"></span><span id="DDK_MSISCSI_NICPERFORMANCE_WMI_CLASS_KR"></span>


MSiSCSI\_NICPerformance WMI クラスは、ネットワーク インターフェイス カード (NIC) のポートのパフォーマンス統計情報を公開します。 このクラスを登録するミニポート ドライバーでは、アダプターのポートごとにクラスの 1 つのインスタンスを作成する必要があります。

イニシエーターは、MSiSCSI の 1 つのインスタンスを実装する必要があります\_NICPerformance クラスの各イーサネット アダプターのポートし、ポートの特定の物理デバイス オブジェクト (PDO) のクラス名の各インスタンスを登録します。

MSiSCSI\_NICPerformance クラスで定義されます*Iscsiprf.mof*します。

```cpp
class MSiSCSI_NICPerformance : Win32_PerfRawData {
  [key] string  InstanceName;
  boolean  Active;
  [read, WmiDataId(1), PerfDefault, 
    CounterType(PERF_COUNTER_COUNTER),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), description("Number of 
    bytes per second transmitted via Ethernet port") : 
    amended] 
    uint32  BytesTransmitted;
  [read, WmiDataId(2), PerfDefault, 
    CounterType(PERF_COUNTER_COUNTER),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), description("Number of 
    bytes per second received via Ethernet port") : amended] 
    uint32  BytesReceived;
  [read, WmiDataId(3), PerfDefault, 
    CounterType(PERF_COUNTER_COUNTER),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), description("Number of 
    bytes per second transmitted via Ethernet port") :
    amended] 
    uint32  PDUTransmitted;
  [read, WmiDataId(4), PerfDefault, 
    CounterType(PERF_COUNTER_COUNTER),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), description("Number of 
    bytes per second received via Ethernet port") : amended]
    uint32  PDUReceived;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_NICPerformance** ](https://msdn.microsoft.com/library/windows/hardware/ff563087)データ構造体。

 

 





