---
title: ndiskd cxadapter
description: Ndiskd cxadapter 拡張機能には、NETADAPTER オブジェクトに関する情報が表示されます。
ms.assetid: 5BE91B1C-9795-4E2C-834A-B7424FF1FCDB
keywords:
- ndiskd cxadapter Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.cxadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ee92f55f7253cdc1000191113f996908d1c2174
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534229"
---
# <a name="ndiskdcxadapter"></a>!ndiskd.cxadapter


**! Ndiskd cxadapter**拡張機能には、netadapter オブジェクトに関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)」を参照してください。

```console
!ndiskd.cxadapter [-handle <x>] [-basic] [-power] [-datapath] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 NETADAPTER のハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
基本情報を表示します。

<span id="_______-power______"></span><span id="_______-POWER______"></span>*-power*   
NETADAPTER の NETPOWERSETTINGS オブジェクトに関する情報を表示します。

<span id="_______-datapath______"></span><span id="_______-DATAPATH______"></span>*-データパス*   
データパスキューに関する情報を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>使用例
--------

NETADAPTER オブジェクトのハンドルを取得するには、最初に[**! ndiskd netadapter**](-ndiskd-netadapter.md)コマンドを実行して、システム上のすべての NIC ドライバーと netadapter の一覧を表示します。 次の例では、Realtek PCIe GBE ファミリコントローラー NetAdapter Sample Driver 2 という名前の NetAdapter のハンドルを探し \# ます。 そのハンドルは ffffd1022d048030 です。

```console
0: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffd1022e8ecae0   ffffd1022d048030    Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    ffffd1022ed908e0   ffffd1022e8611a0    Microsoft Kernel Debug Network Adapter
```

この NetAdapter のハンドルをクリックするか、 **! ndiskd netadapter-handle**コマンドにコマンドラインでハンドルを入力することにより、netadapter オブジェクトなど、この netadapter の詳細を確認できます。 Realtek PCIe GBE ファミリコントローラー NetAdapter サンプルドライバー \# 2 の netadapter ハンドルは、00002efdd0e5f988 です。

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

NETADAPTER オブジェクトは WDF オブジェクトであるため、そのハンドルをクリックすると、デバッガーは[**! wdfkd. wdfkd**](-wdfkd-wdfhandle.md)コマンドを実行します。これにより、WDF の観点から詳細な情報が得られます。 ネットワークの観点から NETADAPTER に関する詳細情報を表示するには、NETADAPTER のハンドルの右側にある [詳細情報] リンクをクリックして、 **! ndiskd cxadapter**コマンドをハンドルで実行します。

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

このコマンドと *-データパス*などの他のパラメーターを組み合わせて、この netadapter の詳細情報を確認することもできます。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワークアダプターの WDF クラス拡張 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!wdfkd.wdfhandle**](-wdfkd-wdfhandle.md)

 

 






