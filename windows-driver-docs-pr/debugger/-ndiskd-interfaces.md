---
title: ndiskd インターフェイス
description: Ndiskd interface 拡張機能には、ネットワークインターフェイスに関する情報が表示されます。
ms.assetid: AC458FDF-CCB6-4A65-8C9C-38C436062017
keywords:
- ndiskd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.interfaces
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fda0e07004abce591f27fe7e91d0a6d21fcf138
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534927"
---
# <a name="ndiskdinterfaces"></a>!ndiskd.interfaces


**! Ndiskd** interface 拡張機能には、ネットワークインターフェイスに関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、すべてのネットワークインターフェイスの一覧が表示されます。

ネットワークインターフェイスの詳細については、「 [NDIS Network インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)」を参照してください。

```console
!ndiskd.interfaces [-handle <x>] [-luid <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
ネットワークインターフェイスのハンドル。

<span id="_______-luid______"></span><span id="_______-LUID______"></span>*-luid*   
ネットワークインターフェイスの[Netluid](https://docs.microsoft.com/windows-hardware/drivers/network/net-luid-value) (ローカルのローカル一意識別子)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

システム上のすべてのネットワークインターフェイスの一覧を表示するには、パラメーターを付けずに **! ndiskd インターフェイス**拡張を実行します。 この例では、Intel (R) 82579LM ギガビットネットワーク接続インターフェイスを探します。 そのハンドルは ffffdf80139f8a20 です。

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

インターフェイスのハンドルをクリックするか、 **! ndiskd handle**コマンドを入力すると、そのインターフェイスの id 情報や現在の状態などの詳細を確認できます。 この例では、Intel (R) 82579LM ギガビットネットワーク接続がイーサネット接続 (ifAlias) であり、接続の MediaConnectUnknown 状態 (Windows カーネルデバッガーで使用するために予約されているため) であることがわかります。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[NDIS ネットワーク インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)

[NET \_ LUID 値](https://docs.microsoft.com/windows-hardware/drivers/network/net-luid-value)

 

 






