---
title: MSiSCSI\_InitiatorLoginStatistics WMI クラス
description: MSiSCSI\_InitiatorLoginStatistics WMI クラス
ms.assetid: cbbfdc11-2c8a-4afa-b62f-187f8c959750
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 059387eb0d3cee259ff723582dbcabff61634da6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370456"
---
# <a name="msiscsiinitiatorloginstatistics-wmi-class"></a>MSiSCSI\_InitiatorLoginStatistics WMI クラス


## <span id="ddk_msiscsi_initiatorloginstatistics_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORLOGINSTATISTICS_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorLoginStatistics WMI クラスは、ログオン統計値を公開します。

このクラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付けられているため、ミニポート ドライバーは、ミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。

MSiSCSI\_InitiatorLoginStatistics クラスで定義されます*Iscsiprf.mof*します。

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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_InitiatorLoginStatistics** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiprf/ns-iscsiprf-_msiscsi_initiatorloginstatistics)データ構造体。

 

 





