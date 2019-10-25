---
title: MSiSCSI\_NICPerformance WMI クラス
description: MSiSCSI\_NICPerformance WMI クラス
ms.assetid: e5894b20-8ea7-46ec-9960-3d9891b06ac4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7becfb7a1a1f42996aa85398c1415cc9b45b5f16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845339"
---
# <a name="msiscsi_nicperformance-wmi-class"></a>MSiSCSI\_NICPerformance WMI クラス


## <span id="ddk_msiscsi_nicperformance_wmi_class_kr"></span><span id="DDK_MSISCSI_NICPERFORMANCE_WMI_CLASS_KR"></span>


MSiSCSI\_NICPerformance WMI クラスは、ネットワークインターフェイスカード (NIC) ポートのパフォーマンス統計情報を公開します。 このクラスを登録するミニポートドライバーは、アダプターのポートごとにクラスのインスタンスを1つ作成する必要があります。

イニシエーターは、アダプターの各イーサネットポートに対して MSiSCSI\_NICPerformance クラスの1つのインスタンスを実装し、クラスの各インスタンスをポートの特定の物理デバイスオブジェクト (PDO) の名前に登録する必要があります。

MSiSCSI\_NICPerformance クラスは*Iscsiprf*で定義されています。

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

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_NICPerformance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_nicperformance)データ構造体を生成します。

 

 





