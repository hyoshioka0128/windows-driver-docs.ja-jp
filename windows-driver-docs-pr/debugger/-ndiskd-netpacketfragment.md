---
title: ndiskd netpacketfragment
description: NET_PACKET_FRAGMENT 構造体に関する情報が表示されます。
ms.assetid: 2075D682-45F5-414D-A8ED-0494B3550C77
keywords:
- ndiskd netpacketfragment Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netpacketfragment
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 41583d17fdf14b150038ab337249df435f3b5b63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837577"
---
# <a name="ndiskdnetpacketfragment"></a>! ndiskd netpacketfragment


**! Ndiskd netpacketfragment**拡張機能には、 [NET\_パケット\_フラグメント](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet-fragment)構造に関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)」を参照してください。

```console
!ndiskd.netpacketfragment [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
必須。 NET\_パケット\_フラグメントのアドレス。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

**  、** [オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)を参照して、NET\_PACKET オブジェクトと NetAdapterCx 内の他のオブジェクトとの関係を説明する図を参照してください。

 

NET\_パケットのハンドルを取得するには、次の手順を実行します。

1.  [ **! Ndiskd netadapter**](-ndiskd-netadapter.md)拡張機能を実行します。
2.  NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3.  NetAdapter の NETADAPTER オブジェクトの右側にある [詳細情報] リンクをクリックして、 [ **! ndiskd cxadapter**](-ndiskd-cxadapter.md)拡張機能を実行します。
4.  *-データパス*パラメーターを指定して **! ndiskd cxadapter**コマンドを入力すると、netadapter のデータパスキューが表示されます。
5.  データパスキューのいずれかのハンドルをクリックします。
6.  データパスキューのリングバッファーのハンドルをクリックします。
7.  リングバッファーの詳細の下部にある [すべての要素の一覧表示] リンクをクリックして、含まれている要素を確認します。
8.  リングバッファーの要素の一覧で、いずれかの[NET\_パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)オブジェクトをクリックします。

この手順の手順1-4 の詳細については、 **! ndiskd cxadapter**トピックの例を参照してください。 この手順の手順5の詳細については、 [ **! ndiskd netqueue**](-ndiskd-netqueue.md)のトピックの例を参照してください。 この手順の手順6-7 の詳細については、 [ **「」の**](-ndiskd-netrb.md)例を参照してください。 この手順の手順8の詳細については、 [ **! ndiskd netpacket**](-ndiskd-netpacket.md)のトピックの例を参照してください。
次の例では、この NET\_PACKET、ffffd1022d000040 の最初のフラグメントのハンドルを探します。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

最初のフラグメントのハンドルをクリックするか、コマンドラインで **! ndiskd netpacketfragment-handle**コマンドを入力して、この NET\_パケット\_フラグメントの詳細を確認できます。これには、仮想アドレス、容量、およびそうでない場合は、NET\_パケットチェーンの最後のパケットであることを示します。

```console
0: kd> !ndiskd.netpacketfragment ffffd1022d000040

    NET_PACKET_FRAGMENT ffffd1022d000040

    Virtual Address    ffffd102303e82f8
    Capacity           0n92
    Valid Length       0n34
    Offset             0n58

    Last packet of chain
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **! ndiskd ヘルプ**](-ndiskd-help.md)

[ネットワークアダプターの WDF クラス拡張 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_パケット\_フラグメント](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet-fragment)

[NET\_パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)

[ **! ndiskd netadapter**](-ndiskd-netadapter.md)

[ **! ndiskd cxadapter**](-ndiskd-cxadapter.md)

[ **! ndiskd netqueue**](-ndiskd-netqueue.md)

[ **! ndiskd netrb**](-ndiskd-netrb.md)

[ **! ndiskd netpacket**](-ndiskd-netpacket.md)

 

 






