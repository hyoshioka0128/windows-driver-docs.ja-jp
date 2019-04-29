---
title: ndiskd.wdiadapter
description: Ndiskd.wdiadapter 拡張機能では、WDIWiFi CAdapter 構造に関する情報が表示されます。 パラメーターなしでこの拡張機能を実行する場合 ndiskd WDIWiFi CAdapter 構造体のすべての一覧が表示されます。
ms.assetid: 1AC069E8-CF87-459B-9C56-DDC1A6F765A8
keywords:
- デバッグ ndiskd.wdiadapter Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.wdiadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36d8b83793d4b8f09e7401084259ed498cb146c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335901"
---
# <a name="ndiskdwdiadapter"></a>!ndiskd.wdiadapter


**! Ndiskd.wdiadapter**拡張機能が、WDIWiFi に関する情報を表示します。CAdapter 構造体。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd すべて WDIWiFi の一覧が表示されます。CAdapter 構造体。

WDI ミニポート ドライバーの詳細については、次を参照してください。、 [WDI ミニポート ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/wdi-miniport-driver-design-guide)します。

WDI ミニポート ドライバー リファレンスの詳細については、次を参照してください。 [WDI ミニポート ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn926075)します。

```console
!ndiskd.wdiadapter [-handle <x>] [-pm] [-rcvfilter] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
CAdapter オブジェクトのハンドル。

<span id="_______-pm______"></span><span id="_______-PM______"></span> *-pm*   
電源管理の状態と機能を示しています。

<span id="_______-rcvfilter______"></span><span id="_______-RCVFILTER______"></span> *-rcvfilter*   
表示には、フィルター処理機能が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>使用例
--------

実行、 **! ndiskd.wdiadapter**ごと、WDI アダプターの詳細情報と共に、すべての CAdapter オブジェクトの一覧を表示するパラメーターなしで拡張機能。 次の例では、1 つだけ CAdapter 構造ですがあります。 関連付けられている、WDI アダプターのハンドルは、ffffc804af396000 です。

```console
1: kd> !ndiskd.wdiadapter
    CAdapter                                                                    
    ffffc804af396000 - WDI Adapter


WDI ADAPTER

    Object             ffffc804af396000
    Miniport           ffffc804b9e6f1a0
    WDI driver         ffffc804b8ce7c40 - WDI MiniDriver
    NetGuid            47cb3aa5-e29c-4628-80bd-5023c53fcccb
    Power              D0

    CCtlPlane          ffffc804af396080
    CTxMgr             ffffc804af399790


DEVICE COMMANDS

    Scheduler state    DeviceCommandSchedulerStateInit
    [No queued device commands found]

Device Command Scheduler


SERIALIZED JOBS

    Job                State               Type               Child             
    ffffc804b9f33000   StepPending         WiFiJobMiniportInitialize



ACTIVE JOBS

    Job                State               Type               Child             
    ffffc804b9f33000   StepPending         WiFiJobMiniportInitialize



EVENTS

    Processing?        No

    Event              Status              Type                                 
    [No events found]

Event Queue


MORE INFORMATION

    Power management                       Receive filtering
```

「電源管理」CAdapter 構造体の説明の下部にある「フィルター処理を受信」のリンクをクリックするか、または入力することができますので、 **! ndiskd.wdiadapter-処理**コマンドかと、 *pm*または *- rcvfilter*オプション。 次の例の出力を示しています、 *- rcvfilter*オプション。

```console
1: kd> !ndiskd.wdiadapter ffffc804af396000 -rcvfilter


RECEIVE FILTER

    Current Configuration

    Revision                               0
    Flags                                  0
    Enabled filter types                   [No flags set]
    Enabled queue types                    [No flags set]
    Max Queues                             0
    Queue properties                       [No flags set]
    Filter tests                           [No flags set]
    Header types                           [No flags set]
    MAC header fields                      [No flags set]
    Max MAC header filters                 0
    Max queue groups                       0
    Max queues per group                   0
    Min lookahead split size               0
    Max lookahead split size               0
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[WDI ミニポート ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/wdi-miniport-driver-design-guide)

[WDI ミニポート ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn926075)

 

 






