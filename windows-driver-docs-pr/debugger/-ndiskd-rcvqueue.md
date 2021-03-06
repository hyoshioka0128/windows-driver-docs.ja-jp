---
title: ndiskd.rcvqueue
description: Ndiskd.rcvqueue コマンドでは、受信キューに関する情報が表示されます。
ms.assetid: 776A459F-A698-4BF6-8DAD-BEB15858AD7F
keywords:
- デバッグ ndiskd.rcvqueue Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.rcvqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b7c4fee97298d7c4d7aadb929fec845d8a42cee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362452"
---
# <a name="ndiskdrcvqueue"></a>!ndiskd.rcvqueue


**! Ndiskd.rcvqueue**コマンドは、受信キューに関する情報を表示します。

```console
!ndiskd.rcvqueue [-handle <x>] [-filters] [-mem] [-verbose] [-rcvqueueverbosity <x>] 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 受信キューのハンドル。

<span id="_______-filters______"></span><span id="_______-FILTERS______"></span> *-フィルター*   
キューにフィルターを示しています。

<span id="_______-mem______"></span><span id="_______-MEM______"></span> *-mem*   
表示は、メモリの割り当てを共有します。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span> *-verbose*   
追加の詳細を示します。

<span id="_______-rcvqueueverbosity______"></span><span id="_______-RCVQUEUEVERBOSITY______"></span> *-rcvqueueverbosity*   
表示する詳細のレベルです。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ndiskd.dll

<a name="examples"></a>例
--------

受信キュー ハンドルを取得するには、まず入力、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)コマンドとパラメーターのないネットワーク アダプター、ドライバー、およびそのハンドルの一覧を参照してください。 次の例では、検索、Microsoft の ISATAP アダプター \#2 の ffff8083e02ce1a0 NetAdapter ハンドル。

```console
3: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffff8083e2668970   ffff8083e02ce1a0    Microsoft ISATAP Adapter #2
    ffff8083e210fae0   ffff8083e0f501a0    Microsoft Kernel Debug Network Adapter
```

次に、ネット アダプターのハンドルを使用して、 **! ndiskd.netadapter-処理 - rcvqueues**そのハンドルと共にこのネット アダプターの受信キューの一覧を取得するコマンド。 この例では、1 つしかない ffff8083e3a3d3a0 のハンドルを持つキュー (いずれかの既定) を受信します。

```console
3: kd> !ndiskd.netadapter ffff8083e02ce1a0 -rcvqueues


RECEIVE QUEUES

    QueueId            Queue Handle        Processor Affinity                   
    0 [Default]        ffff8083e3a3d3a0    0:0000000000000000 (group:mask)
                       Queue Name:         [Zero-length string]
                       VM Name:            [Zero-length string]
```

キュー ハンドルを使用して、受信キューの詳細を確認する、 **! ndiskd.rcvqueue**コマンド。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[ **!ndiskd.netadapter**](-ndiskd-netadapter.md)

 

 






