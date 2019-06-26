---
title: ndiskd.help
description: Ndiskd.help コマンドでは、それぞれの簡単な説明と使用可能な ndiskd コマンドの一覧が表示されます。
ms.assetid: ba9a1364-173b-4258-9894-09271e47786e
keywords:
- デバッグ ndiskd.help Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.help
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f76408e46839fb5d59740adf6bdd0d7504cac470
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364290"
---
# <a name="ndiskdhelp"></a>!ndiskd.help


**! Ndiskd.help**コマンドの使用可能な一覧を表示! ndiskd コマンドは、それぞれの簡単な説明をします。

```console
!ndiskd.help 
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ndiskd.dll

<a name="examples"></a>例
--------

次の例を使用してヘルプ コマンドの一覧を表示する **! ndiskd.help**します。

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

使用して **! ndiskd.help-すべて**、次の例に示すように詳細な一覧を取得します。

**注:**  
いくつか別のコマンドは、この例の下部に一覧表示されます。 これらのコマンドは NDIS ドライバー開発者向けに用意する前にそれらを使用しているユーザーが主要なコマンドを代わりに使用することをお勧めします。



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
    ndisslot           Show an NDIS per-processor slot
    ndis               Show NDIS.sys build info
        dbglevel       Change the debugging level [checked NDIS.sys only]
        dbgsystems     Toggle subsystems being debugged [checked NDIS.sys only]
        ndiskdversion  Show info about NDISKD itself
    netreport          Draw a box diagram of your network stack

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)










