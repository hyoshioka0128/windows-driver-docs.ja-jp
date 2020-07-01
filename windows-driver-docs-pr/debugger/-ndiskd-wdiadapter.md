---
title: ndiskd wdiadapter
description: Ndiskd 拡張機能は、WDIWiFi CAdapter 構造体に関する情報を表示します。 パラメーターを使用せずにこの拡張機能を実行すると、ndiskd には、すべての WDIWiFi CAdapter 構造の一覧が表示されます。
ms.assetid: 1AC069E8-CF87-459B-9C56-DDC1A6F765A8
keywords:
- wdiadapter Windows デバッグ
ms.date: 06/26/2020
topic_type:
- apiref
api_name:
- ndiskd.wdiadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddfa77f65dc81ec5b75b0b6d4b1be426219b6d8b
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593828"
---
# <a name="ndiskdwdiadapter"></a>!ndiskd.wdiadapter

**! Ndiskd**拡張機能は、WDIWiFi に関する情報を表示します。CAdapter 構造体。 パラメーターを使用せずにこの拡張機能を実行すると、! ndiskd にはすべての WDIWiFi の一覧が表示されます。CAdapter 構造体。

WDI ミニポートドライバーの詳細については、「 [WDI ミニポートドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)」を参照してください。

WDI ミニポートドライバーリファレンスの詳細については、「 [WDI ミニポートドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

```console
!ndiskd.wdiadapter [-handle <x>] [-pm] [-rcvfilter] 
```

## <a name="parameters"></a>パラメーター

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
CAdapter オブジェクトの省略可能なハンドル。

<span id="_______-pm______"></span><span id="_______-PM______"></span>*-pm*   
電源管理の状態と機能を表示します。

<span id="_______-rcvfilter______"></span><span id="_______-RCVFILTER______"></span>*-rcvfilter*   
受信フィルター処理機能を示します。

### <a name="dll"></a>[DLL]

Ndiskd.dll

### <a name="examples"></a>例

パラメーターを付けずに **! ndiskd wdiadapter**拡張機能を実行すると、すべての cadapter オブジェクトの一覧と、それぞれの WDI アダプターの詳細が表示されます。 次の例では、CAdapter 構造体が1つしかありません。 関連付けられている WDI アダプターのハンドルは ffffc804af396000 です。

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

ここで、CAdapter 構造の説明の下部にある [電源管理] リンクと [受信フィルター処理] リンクをクリックするか、 *-pm*または *-rcvfilter*オプションを使用して **! ndiskd**コマンドを入力できます。 次の例は、 *-rcvfilter*オプションの出力を示しています。

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

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[WDI ミニポート ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)

[WDI ミニポートドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
