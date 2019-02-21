---
title: ndiskd.netpacketfragment
description: Ndiskd.netpacketfragment 拡張機能では、NET_PACKET_FRAGMENT 構造に関する情報が表示されます。
ms.assetid: 2075D682-45F5-414D-A8ED-0494B3550C77
keywords:
- デバッグ ndiskd.netpacketfragment Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netpacketfragment
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64db59a3e391c12e9aceaeb6bb3b9f6496ff9f59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549200"
---
# <a name="ndiskdnetpacketfragment"></a>! ndiskd.netpacketfragment


**! Ndiskd.netpacketfragment**拡張機能に関する情報を表示する、 [NET\_パケット\_フラグメント](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet-fragment)構造体。

ネットワーク アダプター WDF クラス拡張 (NetAdapterCx) の詳細については、次を参照してください。[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)します。

```console
!ndiskd.netpacketfragment [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 アドレス、NET の\_パケット\_フラグメント。

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
8.  いずれかのクリックして、 [NET\_パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)要素のリング バッファーのリスト内のオブジェクト。

この手順の手順 1 ~ 4 について詳しくは、上の例を参照してください。、 **! ndiskd.cxadapter**トピック。 この手順の手順 5 について詳しくは、上の例を参照してください。、 [ **! ndiskd.netqueue** ](-ndiskd-netqueue.md)トピック。 この手順の手順 6. ~ 7. について詳しくは、上の例を参照してください。、 [ **! ndiskd.netrb** ](-ndiskd-netrb.md)トピック。 この手順の手順 8 について詳しくは、上の例を参照してください。、 [ **! ndiskd.netpacket** ](-ndiskd-netpacket.md)トピック。
次の例でこのネットワークの最初のフラグメントのハンドルを探します\_ffffd1022d000040 パケットの場合。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

最初のフラグメントのハンドルをクリックするかを入力して、 **! ndiskd.netpacketfragment-処理**この NET の詳細を確認することができますが、コマンドラインでコマンド\_パケット\_フラグメントを含む、容量、仮想のアドレス、NET の最後のパケットがかどうかと\_フラグメントのパケットのチェーン。

```console
0: kd> !ndiskd.netpacketfragment ffffd1022d000040

    NET_PACKET_FRAGMENT ffffd1022d000040

    Virtual Address    ffffd102303e82f8
    Capacity           0n92
    Valid Length       0n34
    Offset             0n58

    Last packet of chain
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_パケット\_フラグメント](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet-fragment)

[NET\_パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

[**!ndiskd.netpacket**](-ndiskd-netpacket.md)

 

 






