---
title: ndiskd netrb
description: Ndiskd netrb 拡張機能には、NET_RING 構造に関する情報が表示されます。
ms.assetid: 2D749E7E-00A5-422B-B785-B8DB3393A74F
keywords:
- ndiskd netrb Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netrb
api_type:
- NA
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: da6ec830644af7c8c7abecff5cfcea728e4b9d70
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534907"
---
# <a name="ndiskdnetrb"></a>!ndiskd.netrb


**! Ndiskd netrb**拡張機能には、 [NET \_ RING \_ バッファー](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-ring-buffer)構造に関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)」を参照してください。

```console
!ndiskd.netrb [-handle <x>] [-basic] [-dump] [-elementtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 NET \_ RING バッファーのアドレス \_ 。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
基本情報を表示します。

<span id="_______-dump______"></span><span id="_______-DUMP______"></span>*-ダンプ*   
NET RING バッファー内の各要素に関する情報を表示 \_ \_ します。

<span id="_______-elementtype______"></span><span id="_______-ELEMENTTYPE______"></span>*-elementtype*   
リングバッファー要素を参照するときに使用するデータ型の文字列。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>使用例
--------

**メモ**   「[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)」を参照して、 \_ \_ NetAdapterCx 内の他のオブジェクトとの NET RING バッファーオブジェクトの関係を説明する図を参照してください。

 

NET RING バッファーのハンドルを取得するには、次の \_ \_ 手順を実行します。

1.  [**! Ndiskd netadapter**](-ndiskd-netadapter.md)拡張機能を実行します。
2.  NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3.  NetAdapter の NETADAPTER オブジェクトの右側にある [詳細情報] リンクをクリックして、 [**! ndiskd cxadapter**](-ndiskd-cxadapter.md)拡張機能を実行します。
4.  *-データパス*パラメーターを指定して **! ndiskd cxadapter**コマンドを入力すると、netadapter のデータパスキューが表示されます。
5.  データパスキューのいずれかのハンドルをクリックします。

この手順の手順1-4 の詳細については、 **! ndiskd cxadapter**トピックの例を参照してください。 この手順の手順5の詳細については、 [**! ndiskd netqueue**](-ndiskd-netqueue.md)のトピックの例を参照してください。
次の例では、この NETTXQUEUE のリングバッファーのハンドル ffffd1022d000000 を探します。

```console
0: kd> !ndiskd.netqueue ffffd1022f512700

    NETTXQUEUE         00002efdd0aed9a8
    Ring buffer        ffffd1022d000000

    Switch to EC thread

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtQueueAdvance                        fffff80034152af8   RtEthSample+2af8
    EvtQueueArmNotification                fffff80034159a94   RtEthSample+9a94
    EvtQueueCancel                         fffff800341598d8   RtEthSample+98d8
```

リングバッファーのハンドルをクリックするか、コマンドラインで **! ndiskd. netrb-handle**コマンドを入力することにより、このネットワークリングバッファーの詳細 \_ \_ (含まれる要素の数、開始インデックスと終了インデックスのアドレスなど) を確認できます。

```console
0: kd> !ndiskd.netrb ffffd1022d000000

    NET_RING    ffffd1022d000000

    Number of elements 0x080
    Owned by OS        0x080
    Owned by Client    00000

    Begin Index        0x078 (ffffd1022d003c40 - NET_PACKET)
    Next Index         0x078 (ffffd1022d003c40 - NET_PACKET)
    End Index          0x078 (ffffd1022d003c40 - NET_PACKET)

    List all elements
```

このネット \_ リング \_ バッファーの要素を表示するには、詳細の下部にある [すべての要素を一覧表示する] リンクをクリックするか、コマンドラインで **! ndiskd netrb-dump**コマンドを入力します。 次の例では、簡潔にするために中間要素を excised しています。

```console
0: kd> !ndiskd.netrb ffffd1022d000000 -dump

    [000] ffffd1022d000040 - NET_PACKET
    [001] ffffd1022d0000c0 - NET_PACKET
    [002] ffffd1022d000140 - NET_PACKET
    [003] ffffd1022d0001c0 - NET_PACKET
    [004] ffffd1022d000240 - NET_PACKET
    [005] ffffd1022d0002c0 - NET_PACKET
    
    ...

    [07b] ffffd1022d003dc0 - NET_PACKET
    [07c] ffffd1022d003e40 - NET_PACKET
    [07d] ffffd1022d003ec0 - NET_PACKET
    [07e] ffffd1022d003f40 - NET_PACKET
    [07f] ffffd1022d003fc0 - NET_PACKET
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワークアダプターの WDF クラス拡張 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET \_ RING \_ バッファー](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-ring-buffer)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

 

 






