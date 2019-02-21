---
title: ndiskd.ifstacktable
description: Ndiskd.ifstacktable 拡張機能では、ネットワーク インターフェイスの履歴テーブル (ifStackTable) が表示されます。
ms.assetid: 8166C088-9366-49C4-9C3A-0089807352A9
keywords:
- デバッグ ndiskd.ifstacktable Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ifstacktable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bac729e35a6f350485237b749f28d409f5fbe19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527886"
---
# <a name="ndiskdifstacktable"></a>! ndiskd.ifstacktable


**! Ndiskd.ifstacktable**拡張機能には、ネットワーク インターフェイスの履歴テーブル (ifStackTable) が表示されます。

インターフェイスの履歴テーブルの詳細については、次を参照してください。[ネットワーク インターフェイスのスタックを維持](https://msdn.microsoft.com/windows/hardware/drivers/network/maintaining-a-network-interface-stack)します。

```console
!ndiskd.ifstacktable 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


この拡張機能には、パラメーターがありません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

実行、 **! ndiskd.ifstacktable**コマンドを ifStackTable を参照してください。

```console
3: kd> !ndiskd.ifstacktable


INTERFACE STACK TABLE

    Lower interface    Lower IfIndex       Higher IfIndex     Higher interface  
    ffffdf80139b3a20   6                   15                 ffffdf801494fa20
    ffffdf801494fa20   15                  16                 ffffdf801494c010
    ffffdf801494c010   16                  17                 ffffdf801494ba20
```

NDIS には、NDIS ミニポート アダプター、NDIS 5.x フィルター中間ドライバー、履歴テーブルとは、NDIS フィルター モジュール、 [NDIS MUX 中間ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-mux-intermediate-drivers)内部インターフェイスの関係を指定するドライバーが必要仮想ミニポート インターフェイスとプロトコルの間には、インターフェイスを低きます。 そのため、ifStackTable はより複雑な MUX ドライバーがインストールされていると、システムでインターフェイスのスタックのリレーションシップを表示するための便利なできます。

この例のシステムにインストールされている NDIS MUX 中間のドライバーがないので、ifStackTable のみ NDIS によって提供されるスタック関係を示しています。 次の例の 3 番目の行 (ハンドル ffffdf801494c010、低い IfIndex 16) の下のインターフェイスは、QoS パケット スケジューラのインターフェイスを示しています、ハンドルをクリックします。

```console
3: kd> !ndiskd.interface ffffdf801494c010


INTERFACE

    [Zero-length string]

    Ndis handle        ffffdf801494c010 
    IfProvider         ffffdf80131ca8d0 - The NDIS interface provider
    NDIS filter        ffffdf801494dc70 - Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000

    ifType             IF_TYPE_ETHERNET_CSMACD
    Media type         802.3
    Physical medium    NdisPhysicalMediumOther
    Access type        BROADCAST
    Direction type     SEND_AND_RECEIVE
    Connection type    DEDICATED

    ifConnectorPresent No

    Network            ffffdf80139b8900 - [Unnamed network]
    Compartment        ffffdf80139b9940 - Compartment #1


IDENTIFIERS

    ifAlias            [Zero-length string]
    ifDescr            Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000
    ifName (NET_LUID)  06:01
    ifPhysAddress      18-03-73-c1-e8-72

    ifIndex            0n16
    ifGuid             fc2a0ae1-b103-11e6-b724-806e6f6e6963


STATE

    Connected          Connected
    ifOperStatus       DORMANT
    ifOperStatusFlags  DORMANT_PAUSED

    Link speed         1000000000 (1 Gbps)
    ifMtu              0n1500
    Duplex             FullDuplex

    Refer to RFC 2863 for definitions of many of these terms
```

同じ例では、続行、WFP 802.3 MAC レイヤー ライトウェイト フィルターの 3 番目の行 (ハンドル ffffdf801494ba20 より高い IfIndex 17) の高いインターフェイスにインターフェイスを示しますのハンドルをクリックします。

```console
3: kd> !ndiskd.interface ffffdf801494ba20


INTERFACE

    [Zero-length string]

    Ndis handle        ffffdf801494ba20    [type it]
    IfProvider         ffffdf80131ca8d0 - The NDIS interface provider
    NDIS filter        ffffdf801494c670 - Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000

    ifType             IF_TYPE_ETHERNET_CSMACD
    Media type         802.3
    Physical medium    NdisPhysicalMediumOther
    Access type        BROADCAST
    Direction type     SEND_AND_RECEIVE
    Connection type    DEDICATED

    ifConnectorPresent No

    Network            ffffdf80139b8900 - [Unnamed network]
    Compartment        ffffdf80139b9940 - Compartment #1


IDENTIFIERS

    ifAlias            [Zero-length string]
    ifDescr            Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000
    ifName (NET_LUID)  06:02
    ifPhysAddress      18-03-73-c1-e8-72

    ifIndex            0n17
    ifGuid             fc2a0ae0-b103-11e6-b724-806e6f6e6963


STATE

    Connected          Connected
    ifOperStatus       DORMANT
    ifOperStatusFlags  DORMANT_PAUSED

    Link speed         1000000000 (1 Gbps)
    ifMtu              0n1500
    Duplex             FullDuplex

    Refer to RFC 2863 for definitions of many of these terms
```

これには、WFP 802.3 MAC レイヤー ライトウェイト フィルターがインターフェイスのネットワーク スタックに QoS パケット Scheudler フィルターの上に位置が表示されます。 これを確認するにを実行して、 [ **! ndiskd.netreport** ](-ndiskd-netreport.md)拡張機能では、ネットワーク スタック視覚的にします。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワーク インターフェイスのスタックを維持](https://msdn.microsoft.com/windows/hardware/drivers/network/maintaining-a-network-interface-stack)

[MUX の NDIS 中間ドライバ](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-mux-intermediate-drivers)

[**!ndiskd.netreport**](-ndiskd-netreport.md)

 

 






