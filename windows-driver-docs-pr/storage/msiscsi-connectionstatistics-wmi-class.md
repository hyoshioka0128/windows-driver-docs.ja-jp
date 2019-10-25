---
title: MSiSCSI\_ConnectionStatistics WMI クラス
description: MSiSCSI\_ConnectionStatistics WMI クラス
ms.assetid: f12dfa6a-0999-40a3-9e15-bb65dc086911
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 94a14f9a2b8831f65fa433257733f6842b82426d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845035"
---
# <a name="msiscsi_connectionstatistics-wmi-class"></a>MSiSCSI\_ConnectionStatistics WMI クラス


## <span id="ddk_msiscsi_connectionstatistics_wmi_class_kr"></span><span id="DDK_MSISCSI_CONNECTIONSTATISTICS_WMI_CLASS_KR"></span>


MSiSCSI\_ConnectionStatistics WMI クラスは、接続の統計情報を公開します。 このクラスは、Iscsiprf で次のように定義されています。

```cpp
class MSiSCSI_ConnectionStatistics : Win32_PerfRawData {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [read, WmiDataId(1), WmiVersion(1), 
    cpp_quote(
    "\n    //Text-based identifier for this Initiator that 
    is globally unique.\n"
    "    //The Initiator Name is independent of the location 
    of the initiator.\n"),
    MaxLen(MAX_ISCSI_NAME_LEN)] 
    string  iSCSIName;
  [read, WmiDataId(2), WmiVersion(1), Description("The iSCSI 
    connection ID for this connection instance."): amended] 
    uint16  CID; //session wide namespace
  [read, WmiDataId(3), Description("A uniquely generated 
    session ID used only internally.  Do not mix this with 
    ISID or SSID"): amended,
    cpp_quote(
    "\n    //A uniquely generated session ID used only 
    internally.  Do not mix this with ISID or SSID\n"),
    WmiVersion(1)] 
    uint64  USID;
  [WmiDataId(4), DisplayName("Adapter Id") : amended, 
    DisplayInHex, description("Id that is globally unique to 
    each instance of each adapter. Using the address of the 
    Adapter Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(5), DisplayName("Bytes Sent"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of bytes sent over this 
    connection"): amended] 
    uint64  BytesSent;
  [WmiDataId(6), DisplayName("Bytes Received"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of bytes received over this 
    connection"): amended] 
    uint64  BytesReceived;
  [WmiDataId(7), DisplayName("PDUs Sent"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of  PDU Commands Sent over this 
    connection"): amended] 
    uint64  PDUCommandsSent;
  [WmiDataId(8), DisplayName("PDUs Received"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of PDUResponses received over 
    this connection"): amended] 
    uint64  PDUResponsesReceived;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_ConnectionStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_connectionstatistics)データ構造を生成します。

イニシエーターは、次のターゲットインスタンス名を持つ MSiSCSI\_ConnectionStatistics WMI クラスを登録する必要があります。

```cpp
targetname_#:#
```

最初のシャープ記号 (\#) は、 [**Msiscsi\_ConnectionStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_connectionstatistics)構造体の**usid**メンバーの値です。2番目の番号記号 (\#) は、このクラスの**CID**メンバーの値です。

 

 





