---
title: ndiskd.cxadapter
description: Ndiskd.cxadapter 拡張機能では、NETADAPTER オブジェクトに関する情報が表示されます。
ms.assetid: 5BE91B1C-9795-4E2C-834A-B7424FF1FCDB
keywords:
- デバッグ ndiskd.cxadapter Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.cxadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c84337a548d858c21f9fcf3938bb2d02441c654b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336033"
---
# <a name="ndiskdcxadapter"></a>!ndiskd.cxadapter


**! Ndiskd.cxadapter**拡張機能は、NETADAPTER オブジェクトに関する情報を表示します。

ネットワーク アダプター WDF クラス拡張 (NetAdapterCx) の詳細については、次を参照してください。[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)します。

```console
!ndiskd.cxadapter [-handle <x>] [-basic] [-power] [-datapath] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 NETADAPTER のハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
基本的な情報を表示します。

<span id="_______-power______"></span><span id="_______-POWER______"></span> *電源*   
NETADAPTER NETPOWERSETTINGS オブジェクトに関する情報を表示します。

<span id="_______-datapath______"></span><span id="_______-DATAPATH______"></span> *-datapath*   
データパス キューに関する情報が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>使用例
--------

NETADAPTER オブジェクトのハンドルを取得して最初に実行、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)システム上のすべての NIC ドライバーと NetAdapters 一覧を表示するコマンド。 次の例を探して、ハンドル、NetAdapter Realtek PCIe GBE ファミリ コント ローラー NetAdapter サンプル ドライバーをという名前の\#2。 そのハンドルは、ffffd1022d048030 です。

```console
0: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffd1022e8ecae0   ffffd1022d048030    Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    ffffd1022ed908e0   ffffd1022e8611a0    Microsoft Kernel Debug Network Adapter
```

この NetAdapter のハンドルを入力するかをクリックして、 **! ndiskd.netadapter-処理**コマンドラインでそのハンドルでコマンドをその NETADAPTER オブジェクトを含む、この NetAdapter の詳細を確認することができます。 Realtek PCIe GBE ファミリ コント ローラー NetAdapter サンプル ドライバー \#2 の NETADAPTER ハンドルが 00002efdd0e5f988 します。

```console
0: kd> !ndiskd.netadapter ffffd1022d048030


NETADAPTER

    Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2

    Ndis handle        ffffd1022d048030    
    NETADAPTER         00002efdd0e5f988    More information
    WDFDEVICE          00002efdcf45f2f8
    Driver             ffffd1022e8ecae0 - RtEthSample  v0.0
    Network interface  ffffd1022e395a20

    Media type         802.3
    Device instance    PCI\VEN_10EC&DEV_8168&SUBSYS_816810EC&REV_03\4&22bb23f1&0&0038
    Device object      ffffd1022de127f0    More information
    MAC address        00-e0-4c-68-00-8b


STATE

    Miniport           Running
    Device PnP         Started             Show state history
    Datapath           Normal
    Interface          Up
    Media              Connected
    Power              D0
    References         0n10                Show detail
    Total resets       0
    Pending OID        None
    Flags              NOT_BUS_MASTER, WDF, DEFAULT_PORT_ACTIVATED,
                       SUPPORTS_MEDIA_SENSE, DOES_NOT_DO_LOOPBACK,
                       MEDIA_CONNECTED
    PnP flags          PM_SUPPORTED, DEVICE_POWER_ENABLED,
                       DEVICE_POWER_WAKE_ENABLE, HARDWARE_DEVICE,
                       NDIS_WDM_DRIVER, WAKE_CAPABLE


IP ADDRESS SUMMARY

    10.137.188.169                         See all IP addresses on this adapter
    fe80::3cad:81bb:5dad:1066


BINDINGS

    Protocol list      Driver              Open               Context           
    MSLLDP             ffffd1023043f6a0    ffffd1022e786a90   ffffd102307465c0
    LLTDIO             ffffd1022c6b7830    ffffd1022ef8cc00   ffffd1022f1e5730
    TCPIP6             ffffd1022e2c7c10    ffffd10230b98310   ffffd102304d9010
    (RASPPPOE)         Not running
    (RDMANDK)          ffffd1022d574a70    Declined with NDIS_STATUS_NOT_RECOGNIZED
    RSPNDR             ffffd1022c71a830    ffffd1022de0cc00   ffffd1022d03f6a0
    TCPIP              ffffd1022e2cbc10    ffffd1022de067f0   ffffd1022d03f010
    NDISUIO            ffffd1022de07670    ffffd1022cd648d0   ffffd10231131970

    Filter list        Driver              Module             Context           
    WFP 802.3 MAC Layer LightWeight Filter-0000
                       ffffd1022e384d70    ffffd1022f271660   ffffd10230cfe2c0
    QoS Packet Scheduler-0000
                       ffffd1022d56f220    ffffd1022f26d660   ffffd10231778700
    WFP Native MAC Layer LightWeight Filter-0000
                       ffffd1022e384ad0    ffffd1022f26b660   ffffd1022ed59c20



MORE INFORMATION

    Driver handlers                        Task offloads
    Power management                       PM protocol offloads
    Pending OIDs
    Pending NBLs                           Receive side throttling
    Wake-on-LAN (WoL)                      Packet filter
    Receive queues                         Receive filtering
    RSS                                    NIC switch
                                           Selective suspend
    NDIS ports                             WMI guids
    Diagnostic log
```

NETADAPTER オブジェクトは、WDF オブジェクトでは、そのハンドルをクリックすると、デバッガーを実行する、 [ **! wdfkd.wdfhandle** ](-wdfkd-wdfhandle.md)コマンドを WDF の観点から詳細情報が表示されます。 ネットワークの観点から NETADAPTER に関する詳細情報を表示するを実行する NETADAPTER のハンドルの右側に「詳細」リンクをクリックします。、 **! ndiskd.cxadapter**そのハンドルを持つコマンド。

```console
0: kd> !ndiskd.cxadapter ffffd1022f1a0720


NETADAPTER

    Miniport           ffffd1022d048030 - Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    NETADAPTER         00002efdd0e5f988    
    WDFDEVICE          00002efdcf45f2f8    

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtAdapterCreateTxQueue                fffff80034151508   RtEthSample+1508
    EvtAdapterCreateRxQueue                fffff800341510ec   RtEthSample+10ec

    Show datapath info
    Show NETPOWERSETTINGS info
```

これを組み合わせることもなどその他のパラメーターをコマンド *- データパス*この NETADAPTER の詳細を表示します。

```console
0: kd> !ndiskd.cxadapter ffffd1022f1a0720 -basic -datapath


NETADAPTER

    Miniport           ffffd1022d048030 - Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    NETADAPTER         00002efdd0e5f988    
    WDFDEVICE          00002efdcf45f2f8    

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtAdapterCreateTxQueue                fffff80034151508   RtEthSample+1508
    EvtAdapterCreateRxQueue                fffff800341510ec   RtEthSample+10ec


DATAPATH QUEUES

    NETTXQUEUE         ffffd1022f512700
    NETRXQUEUE         ffffd1022cc7b0d0
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!wdfkd.wdfhandle**](-wdfkd-wdfhandle.md)

 

 






