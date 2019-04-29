---
title: ndiskd.netpacket
description: Ndiskd.netpacket 拡張機能では、NET_PACKET 構造に関する情報が表示されます。
ms.assetid: 304BA2CF-B6BC-452C-8543-9B872054AA9E
keywords:
- デバッグ ndiskd.netpacket Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netpacket
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a7605566839d3962e73a36aaf5689cae1d77dc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335914"
---
# <a name="ndiskdnetpacket"></a>!ndiskd.netpacket


**! Ndiskd.netpacket**拡張機能に関する情報を表示する、 [NET\_パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)構造体。

ネットワーク アダプター WDF クラス拡張 (NetAdapterCx) の詳細については、次を参照してください。[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)します。

```console
!ndiskd.netpacket [-handle <x>] [-basic] [-layout] [-checksum] [-data] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 アドレス、NET の\_パケット。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
基本的な情報を表示します。

<span id="_______-layout______"></span><span id="_______-LAYOUT______"></span> *-layout*   
パケット プロトコル レイアウトを表示します。

<span id="_______-checksum______"></span><span id="_______-CHECKSUM______"></span> *-チェックサム*   
パケット チェックサム情報が表示されます。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-data*   
ペイロードのメモリをダンプします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

**注**  を参照してください[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)NET のリレーションシップを説明する図を参照する\_NetAdapterCx の他のオブジェクトを持つパケット オブジェクト。

 

NET のハンドルを取得する\_パケットの場合、これらの手順に従います。

1.  実行、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)拡張機能。
2.  NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3.  実行する NetAdapter の NETADAPTER オブジェクトの右側に「詳細情報」リンクをクリックして、 [ **! ndiskd.cxadapter** ](-ndiskd-cxadapter.md)拡張機能。
4.  入力、 **! ndiskd.cxadapter**コマンドと、 *- データパス*パラメーターをその NETADAPTER のデータパス キューを参照してください。
5.  データパス キューのいずれかのハンドルをクリックします。
6.  そのデータパス キューのリング バッファーのハンドルをクリックします。
7.  リング バッファーの詳細が含まれている要素を確認するの下部にあるに、「ボックスの一覧のすべての要素」のリンクをクリックします。

この手順の手順 1 ~ 4 について詳しくは、上の例を参照してください。、 **! ndiskd.cxadapter**トピック。 この手順の手順 5 について詳しくは、上の例を参照してください。、 [ **! ndiskd.netqueue** ](-ndiskd-netqueue.md)トピック。 この手順の手順 6. ~ 7. について詳しくは、上の例を参照してください。、 [ **! ndiskd.netrb** ](-ndiskd-netrb.md)トピック。
次の例では、検索、ハンドルの最初の NET\_ffffd1022d000040 パケットの場合。

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

このネットワークに、ハンドルをクリックして\_パケットまたは入力して **! ndiskd.netpacket-処理**、コマンドラインでは、このネットワークの詳細を確認できます\_パケットの場合、それを含んでいるリング バッファーを含む、そのリング バッファーとその最初のフラグメントのハンドルを含むデータパス キュー。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

その他の基本的な説明を組み合わせる **! ndiskd.netpacket**パラメーター、またはそのいずれも、このフラグメントの特定の情報を確認します。 次の例では、すべてのパラメーターを使用します。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040 -basic -layout -checksum -data

    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090


    Protocol Layout                                                             

    Layer 2 Type       ETHERNET
    Header Length      0n14

    Layer 3 Type       IPV4_NO_OPTIONS
    Header Length      0n20

    Layer 4 Type       UDP
    Header Length      8


    Checksum Information                                                        

    Layer 2            TX_PASSTHROUGH
    Layer 3            TX_REQUIRED
    Layer 4            TX_PASSTHROUGH


    Payload data                                                                

    Fragment           ffffd1022d000040
    ffffd102303e8332  00 00 01 02 71 68 0a 89-be 39 e0 00 00 16 94 04  ····qh···9······
    ffffd102303e8342  00 00 22 00 fa 01 00 00-00 01 03 00 00 00 e0 00  ··"·············
    ffffd102303e8352  00 fc   
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

 

 






