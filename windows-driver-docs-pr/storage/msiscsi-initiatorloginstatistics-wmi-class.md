---
title: MSiSCSI\_InitiatorLoginStatistics WMI クラス
description: MSiSCSI\_InitiatorLoginStatistics WMI クラス
ms.assetid: cbbfdc11-2c8a-4afa-b62f-187f8c959750
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fdc41680faf1194a5929c0557612e578249c49ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845355"
---
# <a name="msiscsi_initiatorloginstatistics-wmi-class"></a>MSiSCSI\_InitiatorLoginStatistics WMI クラス


## <span id="ddk_msiscsi_initiatorloginstatistics_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORLOGINSTATISTICS_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorLoginStatistics WMI クラスは、ログオンの統計情報を公開します。

このクラスは記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用してクラスを登録する必要があります。

MSiSCSI\_InitiatorLoginStatistics クラスは*Iscsiprf*で定義されています。

```cpp
class MSiSCSI_InitiatorLoginStatistics : Win32_PerfRawData {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [WmiDataId(1), DisplayName("Adapter Id") : amended, 
    DisplayInHex, description("Id that is globally unique to 
    each instance of each adapter. Using the address of the 
    Adapter Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(2), DisplayName("Login Accept Responses"): 
    amended, PerfDefault, CounterType(0x00010000),
    //    PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of Login Accept Responses"): amended] 
    uint32  LoginAcceptRsps;
  [WmiDataId(3), DisplayName("Login Other Failed Responses") 
    : amended, CounterType(0x00010000),
    //    PERF_COUNTER_RAWCOUNT
    PerfDefault, DefaultScale(0), PerfDetail(100),
    read, Description("Count of Login other failed
    Responses"): amended] 
    uint32 LoginOtherFailRsps;
  [WmiDataId(4), DisplayName("Login Redirect Responses"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Login Redirect Responses"): 
    amended] 
    uint32 LoginRedirectRsps;
  [WmiDataId(5), DisplayName("Login Authentication Failed 
    Responses"): amended, PerfDefault,
    CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Login Authentication Failed 
    Responses"): amended] 
    uint32 LoginAuthFailRsps;
  [WmiDataId(6), DisplayName("Logins  Faiedl (Tar Auth)"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of the number of times a login is 
    aborted due to a target authentication failure"): 
    amended] 
    uint32 LoginAuthenticateFails;
  [WmiDataId(7), DisplayName("Login Negotiation Failed"): 
    amended, PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of the number of times login failed 
    due to negotiation failure with target"): amended] 
    uint32 LoginNegotiateFails;
  [WmiDataId(8), DisplayName("Logout Normal"): amended,
    PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Logout command PDU with reason 
    code 0"): amended] 
    uint32 LogoutNormals;
  [WmiDataId(9), DisplayName("Logout Other Codes"): amended,
    PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("Count of Logout command PDUs with status 
    code other than 0"): amended] 
    uint32 LogoutOtherCodes;
  [WmiDataId(10), DisplayName("Failed Logins"): amended,
    PerfDefault, CounterType(0x00010000),
    // PERF_COUNTER_RAWCOUNT
    DefaultScale(0), PerfDetail(100), read,
    Description("The object counts the number of times a 
    login attempt from this local initiator has failed"): 
    amended] 
    uint32 LoginFailures;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_InitiatorLoginStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_initiatorloginstatistics)データ構造体を生成します。

 

 





