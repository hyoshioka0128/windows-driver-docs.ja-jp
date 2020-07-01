---
title: ndiskd ヘルプ
description: Ndiskd help コマンドを実行すると、使用可能な ndiskd コマンドの一覧と、それぞれの簡単な説明が表示されます。
ms.assetid: ba9a1364-173b-4258-9894-09271e47786e
keywords:
- ndiskd Windows デバッグのヘルプ
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.help
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 71cc9c2f3e291059aef6bc70a84042c135574523
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593946"
---
# <a name="ndiskdhelp"></a>!ndiskd.help

**! Ndiskd help**コマンドを実行すると、使用可能な! ndiskd コマンドの一覧と、それぞれの簡単な説明が表示されます。

```console
!ndiskd.help
```

## <a name="dll"></a>[DLL]

Ndiskd.dll

## <a name="examples"></a>例

次の例では、 **! ndiskd help**を使用してヘルプコマンドの一覧を示します。

```console
3: kd> !ndiskd.help

NDIS KD EXTENSIONS

    help               This help and lots more
    netadapter         Show network adapters  (this is a good starting place)
    protocol           Show protocol drivers
    mopen              Show open bindings between netadapter and protocol
    filter             Show light-weight filters
    nbl                Show information about an NET_BUFFER_LIST
    oid                Show pending OID Requests
    ndis               Show NDIS.sys build info
    netreport          Draw a box diagram of your network stack

    Show more extensions
    View examples & tutorials online
```

を使用すると、次の例に示すように、より詳細な一覧が表示さ**れます。**

**注:**  
この例の下部には、いくつかの代替コマンドが記載されています。 これらのコマンドは、以前に使用した NDIS ドライバー開発者が使用できますが、代わりにプライマリコマンドを使用することをお勧めします。

```console
3: kd> !ndiskd.help -all

NDIS KD EXTENSIONS

    Primary commands:
    help               This help and lots more
    netadapter         Show network adapters  (this is a good starting place)
        minidriver     Show network adapter drivers
        rcvqueue       Show a receive queue (c.f. VMQ)
    protocol           Show protocol drivers
    mopen              Show open bindings between netadapter and protocol
    filter             Show light-weight filters
        filterdriver   Show filter drivers (not to be confused with filters)
    nbl                Show information about an NET_BUFFER_LIST
    nb                 Show information about an NET_BUFFER
    nblpool            Show information about an NET_BUFFER_LIST pool
    nbpool             Show information about an NET_BUFFER pool
    pendingnbls        Show all NET_BUFFER_LISTs that are in transit
    nbllog             Show a log of all NET_BUFFER_LIST activity
    oid                Show pending OID Requests
    interfaces         Show interfaces (à la NDISIF)
        ifprovider     Show registered NDIS interface providers
        ifstacktable   Show the ifStackTable
        networks       Show networks (probably not what you think)
        compartments   Show compartments
    pkt                Show a NDIS_PACKET structure
        pktpools       Show all allocated packet pools
        findpacket     Find a packet in memory
    vc                 Show a CoNDIS virtual connection
    af                 Show a CoNDIS address family
    ndisref            Show a debug log of refcounts
    ndisevent          Show a debug log of events
    ndisstack          Show a debug stack trace
    wdiadapter         Shows one or more WDIWiFi!CAdapter structures
    wdiminidriver      Shows one or more CMiniportDriver structures
    nwadapter          Shows one or more nwifi!ADAPT structures
    ndisrwlock         Show an NDIS_RW_LOCK_EX lock
        dbglevel       Change the debugging level [checked NDIS.sys only]
        dbgsystems     Toggle subsystems being debugged [checked NDIS.sys only]
        ndiskdversion  Show info about NDISKD itself
    netreport          Draw a box diagram of your network stack
    cxadapter          Show information about an NETADAPTER
    netqueue           Show information about a NetAdapterCx datapath queue
    nrc                Show information about an NET_RING_COLLECTION
    netring            Show information about an NET_RING
    netpacket          Show information about an NET_PACKET
    netfragment        Show information about an NET_FRAGMENT

    Alternate commands:
    miniport           Same as !ndiskd.netadapter
    gminiports         Same as !ndiskd.netadapter
    miniports          "Classic" version of !ndiskd.netadapter
    filterdb           Same as !ndiskd.netadapter  -filterdb
    offload            Same as !ndiskd.netadapter  -offloads
    ports              Same as !ndiskd.netadapter  -ports
    rcvqueues          Same as !ndiskd.netadapter  -rcvqueues
    filters            Same as !ndiskd.filter
    opens              Same as !ndiskd.mopen
    protocols          Same as !ndiskd.protocol
    nblpools           Same as !ndiskd.nblpool
    nbpools            Same as !ndiskd.nbpool
```

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)
