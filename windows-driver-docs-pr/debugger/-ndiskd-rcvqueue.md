---
title: ndiskd rcvqueue
description: Ndiskd rcvqueue コマンドは、受信キューに関する情報を表示します。
ms.assetid: 776A459F-A698-4BF6-8DAD-BEB15858AD7F
keywords:
- ndiskd rcvqueue Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.rcvqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d37760a91048660b0f7e15b3bd90be41db83bbbf
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534717"
---
# <a name="ndiskdrcvqueue"></a>!ndiskd.rcvqueue


**! Ndiskd rcvqueue**コマンドは、受信キューに関する情報を表示します。

```console
!ndiskd.rcvqueue [-handle <x>] [-filters] [-mem] [-verbose] [-rcvqueueverbosity <x>] 
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 受信キューのハンドル。

<span id="_______-filters______"></span><span id="_______-FILTERS______"></span>*-フィルター*   
キューのフィルターを表示します。

<span id="_______-mem______"></span><span id="_______-MEM______"></span>*-メモリ*   
共有メモリの割り当てを表示します。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span>*-verbose*   
追加の詳細を表示します。

<span id="_______-rcvqueueverbosity______"></span><span id="_______-RCVQUEUEVERBOSITY______"></span>*-rcvqueueverbosity*   
表示する詳細レベル。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ndiskd .dll

<a name="examples"></a>例
--------

受信キューハンドルを取得するには、まず、パラメーターを指定せずに[**! ndiskd netadapter**](-ndiskd-netadapter.md)コマンドを入力して、ネットアダプター、ドライバー、およびそれらのハンドルの一覧を表示します。 次の例では、Microsoft ISATAP アダプター \# 2 の NetAdapter ハンドル ffff8083e02ce1a0 を探します。

```console
3: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffff8083e2668970   ffff8083e02ce1a0    Microsoft ISATAP Adapter #2
    ffff8083e210fae0   ffff8083e0f501a0    Microsoft Kernel Debug Network Adapter
```

次に、net アダプターのハンドルを使用して、 **! ndiskd. netadapter-handle-rcvqueues**コマンドを使用して、このネットアダプターの受信キューの一覧をハンドルと共に取得します。 この例では、ffff8083e3a3d3a0 のハンドルを持つ受信キューが1つだけ (既定値) 存在します。

```console
3: kd> !ndiskd.netadapter ffff8083e02ce1a0 -rcvqueues


RECEIVE QUEUES

    QueueId            Queue Handle        Processor Affinity                   
    0 [Default]        ffff8083e3a3d3a0    0:0000000000000000 (group:mask)
                       Queue Name:         [Zero-length string]
                       VM Name:            [Zero-length string]
```

キューハンドルを使用して、 **! ndiskd rcvqueue**コマンドで受信キューの詳細を調べることができるようになりました。

```console
3: kd> !ndiskd.rcvqueue ffff8083e3a3d3a0


RECEIVE QUEUE

    [Zero-length string]

    VM name            [Zero-length string]
    QueueId            0
    Ndis handle        ffff8083e3a3d3a0

    Miniport           ffff8083e02ce1a0 - Microsoft ISATAP Adapter #2
    Open               [No associated Open]

    Type               Unspecified
    Flags              [No flags set]
    Allocated          Yes
    References         1

    Num filters        0
    Num buffers hint   0
    MSI-X entry        0
    Lookahead size     0
    Processor affinity 0:0000000000000000 (group:mask)

    Receive filter list
    Shared memory allocations
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

 

 






