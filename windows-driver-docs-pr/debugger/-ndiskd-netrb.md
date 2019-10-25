---
title: ndiskd netrb
description: NET_RING 構造体に関する情報が表示されます。
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
ms.openlocfilehash: 576c721fa9e10d4404d8fda641c445b346426a3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826547"
---
# <a name="ndiskdnetrb"></a>!ndiskd.netrb


**! Ndiskd netrb**拡張機能には、 [NET\_RING\_バッファー](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-ring-buffer)構造に関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)」を参照してください。

```console
!ndiskd.netrb [-handle <x>] [-basic] [-dump] [-elementtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
必須。 \_バッファーの NET\_RING のアドレス。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
基本情報を表示します。

<span id="_______-dump______"></span><span id="_______-DUMP______"></span> *-ダンプ*   
NET\_RING\_BUFFER の各要素に関する情報を表示します。

<span id="_______-elementtype______"></span><span id="_______-ELEMENTTYPE______"></span> *-elementtype*   
リングバッファー要素を参照するときに使用するデータ型の文字列。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

**  、** [オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)を参照して、NET\_リング\_BUFFER オブジェクトと NetAdapterCx 内の他のオブジェクトとの関係を説明する図を参照してください。

 

NET\_RING\_BUFFER のハンドルを取得するには、次の手順を実行します。

1.  [ **! Ndiskd netadapter**](-ndiskd-netadapter.md)拡張機能を実行します。
2.  NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3.  NetAdapter の NETADAPTER オブジェクトの右側にある [詳細情報] リンクをクリックして、 [ **! ndiskd cxadapter**](-ndiskd-cxadapter.md)拡張機能を実行します。
4.  *-データパス*パラメーターを指定して **! ndiskd cxadapter**コマンドを入力すると、netadapter のデータパスキューが表示されます。
5.  データパスキューのいずれかのハンドルをクリックします。

この手順の手順1-4 の詳細については、 **! ndiskd cxadapter**トピックの例を参照してください。 この手順の手順5の詳細については、 [ **! ndiskd netqueue**](-ndiskd-netqueue.md)のトピックの例を参照してください。
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

リングバッファーのハンドルをクリックするか、またはコマンドラインで **! ndiskd. netrb-handle**コマンドを入力して、この NET\_RING\_バッファーの詳細を確認できます。これには、含まれている要素の数や、その Begin と End のアドレスも含まれます。連想.

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

この NET\_リング\_バッファーの要素を確認するには、詳細の下部にある [すべての要素の一覧表示] リンクをクリックするか、コマンドラインで **! ndiskd netrb-dump**コマンドを入力します。 次の例では、簡潔にするために中間要素を excised しています。

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


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **! ndiskd ヘルプ**](-ndiskd-help.md)

[ネットワークアダプターの WDF クラス拡張 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_RING\_バッファー](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-ring-buffer)

[ **! ndiskd netadapter**](-ndiskd-netadapter.md)

[ **! ndiskd cxadapter**](-ndiskd-cxadapter.md)

[ **! ndiskd netqueue**](-ndiskd-netqueue.md)

 

 






