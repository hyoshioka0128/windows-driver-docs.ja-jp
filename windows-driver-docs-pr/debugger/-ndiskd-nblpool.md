---
title: ndiskd ndiskd
description: Ndiskd ndiskd 拡張機能には、NET_BUFFER_LIST (NBL) プールに関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、システム内の割り当てられているすべての NBL プールの一覧が表示されます。
ms.assetid: 78F8E45C-D13D-4628-A387-529291B4C50C
keywords:
- ndiskd. ndiskd Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nblpool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bf10e51debb1dd63c185d759f61dc79277cbb22a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837586"
---
# <a name="ndiskdnblpool"></a>!ndiskd.nblpool


**! Ndiskd ndiskd**拡張機能には、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure) (NBL) プールに関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、システム内の割り当てられているすべての NBL プールの一覧がに表示されます。

```console
!ndiskd.nblpool [-handle <x>] [-basic] [-allocations] [-find <str>] [-findnb <str>] 
    [-findctx <str>] [-findctxtype <str>] [-findva <x>] [-findpa <x>]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
NBL プールのハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
NBL プールに関する基本的な情報を表示します。

<span id="_______-allocations______"></span><span id="_______-ALLOCATIONS______"></span> *-割り当て*   
割り当てられたすべての NBLs を表示します。

<span id="_______-find______"></span><span id="_______-FIND______"></span> *-検索*   
デバッガー式を使用して、割り当てられた NBLs の一覧をフィルター処理します。

<span id="_______-findnb______"></span><span id="_______-FINDNB______"></span> *-findnb*   
リンクされた[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)s (nbs) によって割り当てられた NBLs の一覧をフィルター処理します。

<span id="_______-findctx______"></span><span id="_______-FINDCTX______"></span> *-findctx*   
コンテキスト領域で割り当てられた NBLs の一覧をフィルター処理します。

<span id="_______-findctxtype______"></span><span id="_______-FINDCTXTYPE______"></span> *-findctxtype*   
コンテキスト領域のデータ型をオーバーライドします。

<span id="_______-findva______"></span><span id="_______-FINDVA______"></span> *-findva*   
指定された仮想アドレスをまたがっする NB を含む NBLs を検索します。

<span id="_______-findpa______"></span><span id="_______-FINDPA______"></span> *-findpa*   
指定された物理アドレスをまたがっする NB を含む NBLs を検索します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

すべての割り当て済み NBL プールの一覧を表示するには、パラメーターを指定せずに **! ndiskd ndiskd**コマンドを入力します。 この例では、KDNr タグを使用して、カーネルデバッガーネットワークインターフェイスカード (kdnic) によって割り当てられたプールを探します。 そのハンドルは ffffdf80147e4a40 です。

```console
2: kd> !ndiskd.nblpool
    NBL Pool           Tag                 Allocated by                         
    ffffdf80179b6a40   NiBP                WdNisDrv!CWFPLayer::Initialize+c6
    ffffdf8015ac6a40   EUNP                tunnel!TunnelEtherUdpGlobalInit+81
    ffffdf8015a78040   Nuio                ndisuio!ndisuioCreateBinding+15f
    ffffdf8015a77800   Nuio                ndisuio!ndisuioCreateBinding+13c
    ffffdf8015a63040   BaNB                rspndr!TopStartNetBufferModule+6d
    ffffdf8015a68a40   LLnb                mslldp!lldpProtSetOptions+49
    ffffdf8014654040   BaNB                lltdio!TopStartNetBufferModule+6d
    ffffdf801494ca40   Pcsb                pacer!PcFilterAttach+142
    ffffdf80147e4a40   KDNr                kdnic!NICAllocAdapter+178
    ffffdf80131ce040   bnvW                wfplwfs!DriverEntry+7a0
    ffffdf80139ffa40   Wfdp                wfplwfs!WfpRioInitialize+a4
    ffffdf8012061200   UNbl                NETIO!NetioAllocateNetBufferListNetBufferMdlAndDataPool+49
    ffffdf8013968a40   TcDN                NETIO!NetioAllocateNetBufferListNetBufferMdlAndDataPool+49
    ffffdf8013969a40   TNbl                NETIO!NetioAllocateNetBufferListNetBufferMdlAndDataPool+49
    ffffdf801397c040   StBn                NETIO!StreamPoolsInit+c1
    ffffdf8013088040   Wfra                NETIO!WfpNblInfoLibraryInit+b8
    ffffdf8012067440   Nnnn                NETIO!NetioInitializeNetBufferListLibrary+13e
    ffffdf8012067a40   Nnbl                NETIO!NetioInitializeNetBufferListLibrary+112
    ffffdf80131caa40   NDrt                ndis!ndisInitializePeriodicReceives+22f
    ffffdf80131d5a40   NDnd                ndis!DriverEntry+5e9
```

NBL プールのハンドルをクリックするか、 **! ndiskd ndiskd-handle**コマンドを入力して詳細を確認します。

```console
2: kd> !ndiskd.nblpool ffffdf80147e4a40


NBL POOL

    Ndis handle        ffffdf80147e4a40
    Allocation tag     KDNr
    Owner
    Allocated by       kdnic!NICAllocAdapter+178

    Flags              CONTAINS_NET_BUFFER
    Structure size     0n544
    Context size       0
    Data size          0

    All allocated NBLs
```

この NBL pool に含まれる NBLs を調べるには、下部にある [割り当て済みのすべての NBLs] リンクをクリックします。 または、 **! ndiskd. ndiskd-handle-割り当て**コマンドを入力することもできます。 次の例に示すように、この NBL pool には1024以上の NBLs が含まれているため、ndiskd は早期に終了します。 -Force オプションを使用してこの制限を回避し、この NBL プールのすべての NBLs を確認できます。

```console
2: kd> !ndiskd.nblpool ffffdf80147e4a40 -allocations


ALL ALLOCATED NBLs

    NBL                Active?                                                  
    ffffdf8014951940   Allocated
    ffffdf8014951b90   Allocated
    ffffdf8014951de0   Allocated
    ffffdf8014951030   Allocated
    ffffdf80149524a0   Allocated
    ffffdf80149526f0   Allocated
    ffffdf8014952940   Allocated
    ffffdf8014952b90   Allocated
    ffffdf8014952de0   Allocated
    ffffdf8014952030   Allocated
    ffffdf80149534a0   Allocated
    ffffdf80149536f0   Allocated
    ffffdf8014953940   Allocated
    ffffdf8014953b90   Allocated
    ffffdf8014953de0   Allocated
    ffffdf8014953030   Allocated
    ffffdf80149544a0   Allocated
    ffffdf80149546f0   Allocated
    ffffdf8014954940   Allocated

...

    ffffdf80148b0b90   Allocated
    ffffdf80148b0de0   Allocated
    ffffdf80148b0030   Allocated
    ffffdf80148b14a0   Allocated
    ffffdf80148b16f0   Allocated
    ffffdf80148b1940   Allocated
    ffffdf80148b1b90   Allocated
    ffffdf80148b1de0   Allocated
    ffffdf80148b1030   Allocated
    [Maximum of 1024 items read; quitting early. Rerun with the '-force' option
    to bypass this limit.]
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

 

 






