---
title: ndiskd ifstacktable
description: Ndiskd ifstacktable 拡張機能により、ネットワークインターフェイススタックテーブル (ifStackTable) が表示されます。
ms.assetid: 8166C088-9366-49C4-9C3A-0089807352A9
keywords:
- ndiskd ifstacktable Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ifstacktable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 45b17f6bfeebce573a847d9c917571b7ee1edf4f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826658"
---
# <a name="ndiskdifstacktable"></a>!ndiskd.ifstacktable


**! Ndiskd ifstacktable**拡張機能により、ネットワークインターフェイススタックテーブル (ifstacktable) が表示されます。

インターフェイススタックテーブルの詳細については、「[ネットワークインターフェイススタックの保守](https://docs.microsoft.com/windows-hardware/drivers/network/maintaining-a-network-interface-stack)」を参照してください。

```console
!ndiskd.ifstacktable 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


この拡張機能にはパラメーターがありません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

IfStackTable を表示するには、 **! ndiskd ifstacktable**コマンドを実行します。

```console
3: kd> !ndiskd.ifstacktable


INTERFACE STACK TABLE

    Lower interface    Lower IfIndex       Higher IfIndex     Higher interface  
    ffffdf80139b3a20   6                   15                 ffffdf801494fa20
    ffffdf801494fa20   15                  16                 ffffdf801494c010
    ffffdf801494c010   16                  17                 ffffdf801494ba20
```

Ndis は、ndis ミニポートアダプター、NDIS 5.x フィルター中間ドライバー、および NDIS フィルターモジュールのスタックテーブルを保持します。一方、ndis [MUX 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)ドライバーは、仮想デバイス間の内部インターフェイス関係を指定するために必要です。ミニポートインターフェイスとプロトコル下位インターフェイス。 したがって、ifStackTable は、より複雑な MUX ドライバーがインストールされているシステムで、インターフェイススタックの関係を確認するのに役立ちます。

この例のシステムには NDIS MUX 中間ドライバーがインストールされていないため、ifStackTable では、NDIS が提供しているスタック関係のみが表示されます。 次の例では、3番目の行の下位インターフェイス (handle ffffdf801494c010、Lower IfIndex 16) のハンドルをクリックすると、QoS パケットスケジューラのインターフェイスが表示されます。

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

同じ例を続けて、3番目の行の上位のインターフェイス (handle ffffdf801494ba20, IfIndex 17) のハンドルをクリックすると、WFP 802.3 MAC レイヤーライトウェイトフィルターのインターフェイスが表示されます。

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

これは、WFP 802.3 MAC レイヤーライトウェイトフィルタがネットワークインターフェイススタックの QoS パケット Scheudler フィルタの上にあることを示しています。 これを確認するには、 [ **! ndiskd netreport**](-ndiskd-netreport.md)拡張機能を実行します。これにより、ネットワークスタックが視覚的に表示されます。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **! ndiskd ヘルプ**](-ndiskd-help.md)

[ネットワークインターフェイススタックの保守](https://docs.microsoft.com/windows-hardware/drivers/network/maintaining-a-network-interface-stack)

[NDIS MUX 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)

[ **! ndiskd netreport**](-ndiskd-netreport.md)

 

 






