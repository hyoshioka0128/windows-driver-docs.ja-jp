---
title: ndiskd.ndisevent
description: '! Ndiskd.ndisevent 拡張機能は、NDIS デバッグ イベント ログを表示します。'
ms.assetid: E042CA22-6521-4DD4-9396-39EC587706D6
keywords:
- デバッグ ndiskd.ndisevent Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisevent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6aa21c8574d636afae2cfc782ab2c6cbeda70db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362492"
---
# <a name="ndiskdndisevent"></a>!ndiskd.ndisevent


**注**  サード パーティ製ネットワーク ドライバー開発者が手動でこの拡張機能のコマンドを使用する必要はありません。 表示される情報を表示することを行うことができますが、ドライバー、詳細を再利用できません。

 

**! Ndiskd.ndisevent**拡張機能は、NDIS デバッグ イベント ログを表示します。

```console
!ndiskd.ndisevent [-handle <x>] [-tagtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 イベント ログのハンドル。

<span id="_______-tagtype______"></span><span id="_______-TAGTYPE______"></span> *-tagtype*   
タグの列挙型。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

ネットワーク アダプターの場合、イベント ログの出力を表示する! ndiskd 提供へのリンクの状態 セクションで、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)出力します。 これはミニポート ブロックからのイベント ログのハンドルを検索および実行に使用するは、手動の方法より簡単、 **! ndiskd.ndisevent**拡張機能。

最初に、入力、 **! ndiskd.netadapter**コマンドとパラメーターのないシステムのネットワーク アダプターおよびミニポート ドライバーの一覧を参照してください。 次の例には、もの AVASTAR ワイヤレス AC ネットワーク コント ローラー、ffffc804b9e6f1a0 のハンドルを探します。

```console
1: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffc804af2e3710   ffffc804b9e6f1a0    Marvell AVASTAR Wireless-AC Network Controller
    ffffc804b99b9020   ffffc804b9c301a0    WAN Miniport (Network Monitor)
    ffffc804b99b9020   ffffc804b9c2a1a0    WAN Miniport (IPv6)
    ffffc804b99b9020   ffffc804b8a8a1a0    WAN Miniport (IP)
    ffffc804ae9d7020   ffffc804b9ceb1a0    WAN Miniport (PPPOE)
    ffffc804b9ca5900   ffffc804b9e601a0    WAN Miniport (PPTP)
    ffffc804b99dc720   ffffc804b99b01a0    WAN Miniport (L2TP)
    ffffc804b86581b0   ffffc804b9c6c1a0    WAN Miniport (IKEv2)
    ffffc804ad4a7250   ffffc804b99651a0    WAN Miniport (SSTP)
    ffffc804b11c4020   ffffc804b85821a0    Microsoft ISATAP Adapter
    ffffc804b11c4020   ffffc804b71731a0    Microsoft ISATAP Adapter #2
    ffffc804ad725020   ffffc804b05e71a0    Surface Ethernet Adapter #2
    ffffc804b0bf0020   ffffc804b0c011a0    Bluetooth Device (Personal Area Network)
    ffffc804aef695e0   ffffc804aed331a0    TAP-Windows Adapter V9
```

ここで、その NetAdapter はリンクをクリックしてまたは入力、 **! ndiskd.netadapter-処理**コマンドをその詳細を参照してください。 状態 セクションで、デバイスの PnP フィールドの右側に「状態の履歴を表示する」リンクを探します。

```console
1: kd> !ndiskd.netadapter ffffc804b9e6f1a0


MINIPORT

    Marvell AVASTAR Wireless-AC Network Controller

    Ndis handle        ffffc804b9e6f1a0
    Ndis API version   v6.50
    Adapter context    ffffc804af3b1100
    Driver             ffffc804af2e3710 - mrvlpcie8897  v1.0
    Network interface  ffffc804aea60a20

    Media type         802.3
    Physical medium    NdisPhysicalMediumUnspecified
    Device instance    PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0001&REV_00\4&379f07b2&0&00E0
    Device object      ffffc804b9e6f050    More information
    MAC address        c0-33-5e-13-22-f7


STATE

    Miniport           INITIALIZING
    Device PnP         ADDED               Show state history
    Datapath           Normal
    Operational status DOWN
    Operational flags  [No flags set]
    Admin status       ADMIN_UP
    Media              MediaConnectUnknown
    Power              D0
    References         1                   Show detail
    Total resets       0
    Pending OID        None
    Flags              IN_INITIALIZE, NOT_BUS_MASTER, DEFAULT_PORT_ACTIVATED,
                       NOT_SUPPORTS_MEDIA_SENSE, DOES_LOOPBACK, MEDIA_CONNECTED
    PnP flags          PM_SUPPORTED, RECEIVED_START, HARDWARE_DEVICE


WDI

    This system supports WDI.
    Learn more about the associated WDI state


BINDINGS

    Protocol list      Driver              Open               Context           
    No protocols are bound to this miniport

    Filter list        Driver              Module             Context           
    No filters are bound to this miniport



MORE INFORMATION

    Driver handlers                        Task offloads
    Power management                       PM protocol offloads
    Pending OIDs                           Timers
    Pending NBLs                           Receive side throttling
    Wake-on-LAN (WoL)                      Packet filter
    Receive queues                         Receive filtering
    RSS                                    NIC switch
    Hardware resources                     Selective suspend
    NDIS ports                             WMI guids
    Diagnostic log
```

「状態の履歴を表示する」リンクをクリックします。 または、ネット アダプターのハンドルを使用して入力できますので、 **! ndiskd.netadapter-処理 - ログ**コマンドで、このミニポートのミニポート ドライバーの PnP、イベント ログを表示します。

```console
1: kd> !ndiskd.netadapter ffffc804b9e6f1a0 -log


MINIPORT PM & PNP EVENTS

    Event              Timestamp           (most recent event at bottom)        
    DeviceAdded
                       13 ms later
    DeviceStart
                       Mon Mar 20 21:27:07.106 2017 (UTC - 7:00) Now?

    Set a breakpoint on the next event
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[ **!ndiskd.netadapter**](-ndiskd-netadapter.md)

 

 






