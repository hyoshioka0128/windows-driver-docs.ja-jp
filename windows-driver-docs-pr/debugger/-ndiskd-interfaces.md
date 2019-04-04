---
title: ndiskd.interfaces
description: Ndiskd.interfaces 拡張機能では、ネットワーク インターフェイスに関する情報が表示されます。
ms.assetid: AC458FDF-CCB6-4A65-8C9C-38C436062017
keywords:
- デバッグ ndiskd.interfaces Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.interfaces
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd9407a23995113b7fde4e7d613607621d334c01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558026"
---
# <a name="ndiskdinterfaces"></a>! ndiskd.interfaces


**! Ndiskd.interfaces**拡張機能は、ネットワーク インターフェイスに関する情報を表示します。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd すべてのネットワーク インターフェイスの一覧が表示されます。

ネットワーク インターフェイスの詳細については、[ネットワーク インターフェイスの NDIS](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-network-interfaces2)を参照してください。

```console
!ndiskd.interfaces [-handle <x>] [-luid <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
ネットワーク インターフェイスのハンドル。

<span id="_______-luid______"></span><span id="_______-LUID______"></span> *-luid*   
[NetLuid](https://msdn.microsoft.com/windows/hardware/drivers/network/net-luid-value) (Net ローカル一意識別子) のネットワーク インターフェイス。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

実行、 **! ndiskd.interfaces**システム上のすべてのネットワーク インターフェイスの一覧を表示するパラメーターなしで拡張機能。 この例では、intel (r) 82579 lm ギガビット ネットワーク接続のインターフェイスを探します。 そのハンドルは、ffffdf80139f8a20 です。

```console
1: kd> !ndiskd.interfaces
    Interface                                                                   
    ffffdf801494fa20 - Microsoft Kernel Debug Network Adapter-WFP Native MAC Layer LightWeight Filter-0000
    ffffdf801494c010 - Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000
    ffffdf801494ba20 - Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000
    ffffdf80139b3a20 - Microsoft Kernel Debug Network Adapter
    ffffdf80139f8a20 - Intel(R) 82579LM Gigabit Network Connection
    ffffdf80139baa20 - WAN Miniport (IP)
    ffffdf80139a4a20 - WAN Miniport (IPv6)
    ffffdf80131d0010 - WAN Miniport (Network Monitor)
    ffffdf80131cda20 - WAN Miniport (PPPOE)
    ffffdf80139b6a20 - Software Loopback Interface 1
    ffffdf80139b0a20 - Microsoft ISATAP Adapter
    ffffdf80139ada20 - WAN Miniport (SSTP)
    ffffdf80131cf010 - WAN Miniport (IKEv2)
    ffffdf80139fea20 - WAN Miniport (L2TP)
    ffffdf80139a7a20 - WAN Miniport (PPTP)
    ffffdf80139aaa20 - Microsoft ISATAP Adapter #2
    ffffdf80139fba20 - Teredo Tunneling Pseudo-Interface
```

入力することも、インターフェイスのハンドルをクリックして、 **! ndiskd.interfaces-処理**コマンド、その識別子情報や現在の状態など、そのインターフェイスについての詳細を確認できます。 この例では、intel (r) 82579 lm ギガビット ネットワーク接続、イーサネット接続 (その ifAlias) し、(Windows のカーネル デバッガーによって用に予約されていますが)、その接続の MediaConnectUnknown 状態にあることを確認できます。

```console
1: kd> !ndiskd.interfaces ffffdf80139f8a20


INTERFACE

    Ethernet

    Ndis handle        ffffdf80139f8a20
    IfProvider         ffffdf80131ca8d0 - The NDIS interface provider
    Provider context   ffffdf80139f8a20

    ifType             IF_TYPE_ETHERNET_CSMACD
    Media type         802.3
    Physical medium    802.3
    Access type        BROADCAST
    Direction type     SEND_AND_RECEIVE
    Connection type    DEDICATED

    ifConnectorPresent No

    Network            ffffdf80139b8900 - [Unnamed network]
    Compartment        ffffdf80139b9940 - Compartment #1


IDENTIFIERS

    ifAlias            Ethernet
    ifDescr            Intel(R) 82579LM Gigabit Network Connection
    ifName (NET_LUID)  06:8001
    ifPhysAddress      18-03-73-c1-e8-72

    ifIndex            0n14
    ifGuid             cbddfde1-5570-4c65-9d47-52d63abce00c


STATE

    Connected          MediaConnectUnknown
    ifOperStatus       NOT_PRESENT

    Link speed         0 [Speed is not applicable]
    ifMtu              0
    Duplex             UnknownDuplex

    Refer to RFC 2863 for definitions of many of these terms
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワークの NDIS インターフェイス](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-network-interfaces2)

[NET\_LUID 値](https://msdn.microsoft.com/windows/hardware/drivers/network/net-luid-value)

 

 






