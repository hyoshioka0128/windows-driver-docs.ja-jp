---
title: MSiSCSI\_NICPerformance WMI クラス
description: MSiSCSI\_NICPerformance WMI クラス
ms.assetid: e5894b20-8ea7-46ec-9960-3d9891b06ac4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ca5e3f078daf9ea59bcb4bccf0a1a7df2d949174
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385832"
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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_NICPerformance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiprf/ns-iscsiprf-_msiscsi_nicperformance)データ構造体。

 

 





