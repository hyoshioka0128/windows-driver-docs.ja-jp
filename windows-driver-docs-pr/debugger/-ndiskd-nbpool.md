---
title: ndiskd.nbpool
description: Ndiskd.nbpool 拡張機能では、NET_BUFFER (NB) プールに関する情報が表示されます。
ms.assetid: 4FCD48B7-C469-4057-A279-20522B00E80B
keywords:
- デバッグ ndiskd.nbpool Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbpool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb374611ea34d06b6ddb1ebc1f411b4e8e424aaa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574015"
---
# <a name="ndiskdnbpool"></a>!ndiskd.nbpool


**! Ndiskd.nbpool**拡張機能に関する情報を表示する、 [ **NET\_バッファー** ](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-structure) (NB) プール。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd はシステムに割り当てられているすべての NB プールの一覧を表示します。

```console
!ndiskd.nbpool [-handle <x>] [-allocations] [-find <str>] [-findva <x>] [-findpa <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NB プールのハンドル。

<span id="_______-allocations______"></span><span id="_______-ALLOCATIONS______"></span> *-allocations*   
すべての表示には、おり、nbs 経由が割り当てられます。

<span id="_______-find______"></span><span id="_______-FIND______"></span> *-検索*   
デバッガー式を使用して割り当てられたおり、nbs 経由の一覧をフィルター処理します。

<span id="_______-findva______"></span><span id="_______-FINDVA______"></span> *-findva*   
指定した仮想アドレスにまたがるおり、nbs 経由を検索します。

<span id="_______-findpa______"></span><span id="_______-FINDPA______"></span> *-findpa*   
特定の物理アドレスにまたがるおり、nbs 経由を検索します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>使用例
--------

入力、 **! ndiskd.nbpool**コマンドとパラメーターのないすべての割り当てられた NB プールの一覧を参照してください。 この例では、Nnbf タグを持つ Netio サービスによって割り当てられた NB プールを探します。 そのハンドルは、ffffdf801308ca40 です。

```console
2: kd> !ndiskd.nbpool
    NB Pool            Tag                 Allocated by                         
    ffffdf8013963a40   UDNb                NETIO!NetioAllocateNetBufferMdlAndDataPool+3c
    ffffdf801396aa40   TSNb                NETIO!NetioAllocateNetBufferMdlAndDataPool+3c
    ffffdf801397d4c0   StBn                NETIO!StreamPoolsInit+90
    ffffdf801308ca40   Nnbf                NETIO!NetioInitializeNetBufferListLibrary+dd
    ffffdf80131cba40   NDnd                ndis!DriverEntry+615
```

NB プールのハンドルをクリックするか、入力、 **! ndiskd.nbpool-処理**コマンドの詳細を確認します。

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

この NB プールに含まれている、おり、nbs 経由を調べるには、下部にある「すべての割り当てられたおり、nbs 経由」のリンクをクリックします。 また、入力することも、 **! ndiskd.nbpool-処理 - 割り当て**コマンド。 次の例に示すようにこの NB プールが含まれる 1024 を超えており、nbs 経由のため! ndiskd が早期に終了します。 使用することができます force オプションを指定するには、この制限を回避しており、この NB プール nbs 経由のすべてを参照してください。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NET\_バッファー**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-structure)

 

 






