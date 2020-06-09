---
title: ndiskd nbpool
description: Ndiskd nbpool 拡張機能には、NET_BUFFER (NB) プールに関する情報が表示されます。
ms.assetid: 4FCD48B7-C469-4057-A279-20522B00E80B
keywords:
- ndiskd nbpool Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbpool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73a23317652e33db9420e46a18bb8ab92cfddaf3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534201"
---
# <a name="ndiskdnbpool"></a>!ndiskd.nbpool


**! Ndiskd nbpool**拡張機能には、 [**NET \_ BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure) (NB) プールに関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、システムに割り当てられているすべての NB プールの一覧がに表示されます。

```console
!ndiskd.nbpool [-handle <x>] [-allocations] [-find <str>] [-findva <x>] [-findpa <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
NB プールのハンドル。

<span id="_______-allocations______"></span><span id="_______-ALLOCATIONS______"></span>*-割り当て*   
割り当てられたすべての NBs を表示します。

<span id="_______-find______"></span><span id="_______-FIND______"></span>*-検索*   
デバッガー式を使用して、割り当てられた NBs の一覧をフィルター処理します。

<span id="_______-findva______"></span><span id="_______-FINDVA______"></span>*-findva*   
指定された仮想アドレスをまたがるする NBs を検索します。

<span id="_______-findpa______"></span><span id="_______-FINDPA______"></span>*-findpa*   
指定された物理アドレスをまたがるする NBs を検索します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

割り当てられているすべての NB プールの一覧を表示するには、パラメーターを指定せずに **! ndiskd nbpool**コマンドを入力します。 この例では、Netio サービスによって、Nnbf タグを使用して割り当てられた NB プールを探します。 そのハンドルは ffffdf801308ca40 です。

```console
2: kd> !ndiskd.nbpool
    NB Pool            Tag                 Allocated by                         
    ffffdf8013963a40   UDNb                NETIO!NetioAllocateNetBufferMdlAndDataPool+3c
    ffffdf801396aa40   TSNb                NETIO!NetioAllocateNetBufferMdlAndDataPool+3c
    ffffdf801397d4c0   StBn                NETIO!StreamPoolsInit+90
    ffffdf801308ca40   Nnbf                NETIO!NetioInitializeNetBufferListLibrary+dd
    ffffdf80131cba40   NDnd                ndis!DriverEntry+615
```

NB プールのハンドルをクリックするか、 **! ndiskd. nbpool-handle**コマンドを入力して詳細を確認します。

```console
2: kd> !ndiskd.nbpool ffffdf801308ca40


NB POOL

    Ndis handle        ffffdf801308ca40
    Allocation tag     Nnbf
    Owner
    Allocated by       NETIO!NetioInitializeNetBufferListLibrary+dd

    Flags              [No flags set]
    Structure size     0n176
    Data size          0

    All allocated NBs
```

この NB プールに含まれる NBs を探索するには、下部にある [割り当て済みのすべての NBs] リンクをクリックします。 または、 **! ndiskd. nbpool-ハンドル割り当て**コマンドを入力することもできます。 次の例に示すように、この NB プールには1024を超える NBs が含まれています。 ndiskd は早期に終了します。 -Force オプションを使用してこの制限を回避し、この NB プール内のすべての NBs を表示できます。

```console
2: kd> !ndiskd.nbpool ffffdf801308ca40 -allocations


ALL ALLOCATED NBs

    NB                 Active?                                                  
    ffffdf8016ea4360   Allocated
    ffffdf801744df50   Allocated
    ffffdf8016932860   Allocated
    ffffdf8016e31500   Allocated
    ffffdf80174eade0   Allocated
    ffffdf8017daa900   Allocated
    ffffdf8017c8c680   Allocated
    ffffdf80166b23b0   Allocated
    ffffdf80164fea70   Allocated
    ffffdf8012845990   Allocated
    ffffdf8017d692d0   Allocated
    ffffdf8017cdc090   Allocated
    ffffdf8012771780   Allocated
    ffffdf80158a3550   Allocated
    ffffdf8012eef5c0   Allocated
    ffffdf80127719d0   Allocated
    ffffdf8015119570   Allocated
    ffffdf8012e18d40   Allocated
    ffffdf8017929b10   Allocated
    ffffdf8016d4e430   Allocated

...

    ffffdf8015ffbbd0   Allocated
    ffffdf8015ec1b10   Freed
    ffffdf80158e56d0   Allocated
    ffffdf8016272110   Freed
    ffffdf8015d8e030   Freed
    ffffdf8015d8e770   Freed
    ffffdf80158ddc30   Freed
    ffffdf801584acc0   Freed
    ffffdf8015846b40   Freed
    ffffdf8015a06c50   Freed
    ffffdf801480c300   Freed
    ffffdf8015e48f50   Freed
    ffffdf8015de64e0   Freed
    ffffdf8015ddff50   Freed
    [Maximum of 1024 items read; quitting early. Rerun with the '-force' option
    to bypass this limit.]
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NET \_ バッファー**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

 

 






