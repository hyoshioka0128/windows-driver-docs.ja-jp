---
title: ndiskd.netrb
description: Ndiskd.netrb 拡張機能では、NET_RING_BUFFER 構造に関する情報が表示されます。
ms.assetid: 2D749E7E-00A5-422B-B785-B8DB3393A74F
keywords:
- デバッグ ndiskd.netrb Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netrb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1089b6a3fa623d23b83fe40910935cace07d7c32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551284"
---
# <a name="ndiskdnetrb"></a>!ndiskd.netrb


**! Ndiskd.netrb**拡張機能に関する情報を表示する、 [NET\_リング\_バッファー](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-ring-buffer)構造体。

ネットワーク アダプター WDF クラス拡張 (NetAdapterCx) の詳細については、次を参照してください。[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)します。

```console
!ndiskd.netrb [-handle <x>] [-basic] [-dump] [-elementtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 アドレス、NET の\_リング\_バッファー。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
基本的な情報を表示します。

<span id="_______-dump______"></span><span id="_______-DUMP______"></span> *-dump*   
NET の各要素に関する情報を表示します。\_リング\_バッファー。

<span id="_______-elementtype______"></span><span id="_______-ELEMENTTYPE______"></span> *-elementtype*   
リング バッファーの要素を参照するときに使用するデータ型の文字列。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

**注**  を参照してください[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)NET のリレーションシップを説明する図を参照する\_リング\_NetAdapterCx の他のオブジェクトのバッファー オブジェクト。

 

NET のハンドルを取得する\_リング\_バッファー、これらの手順に従います。

1.  実行、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)拡張機能。
2.  NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3.  実行する NetAdapter の NETADAPTER オブジェクトの右側に「詳細情報」リンクをクリックして、 [ **! ndiskd.cxadapter** ](-ndiskd-cxadapter.md)拡張機能。
4.  入力、 **! ndiskd.cxadapter**コマンドと、 *- データパス*パラメーターをその NETADAPTER のデータパス キューを参照してください。
5.  データパス キューのいずれかのハンドルをクリックします。

この手順の手順 1 ~ 4 について詳しくは、上の例を参照してください。、 **! ndiskd.cxadapter**トピック。 この手順の手順 5 について詳しくは、上の例を参照してください。、 [ **! ndiskd.netqueue** ](-ndiskd-netqueue.md)トピック。
次の例では、この NETTXQUEUE のリング バッファー、ffffd1022d000000 のハンドルを探します。

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

リング バッファーを入力するか、ハンドルをクリックして、 **! ndiskd.netrb-処理**この NET の詳細を確認することができますが、コマンドラインでコマンド\_リング\_が含まれている要素の数を含むバッファーその開始と終了インデックスのアドレス。

```console
0: kd> !ndiskd.netrb ffffd1022d000000

    NET_RING_BUFFER    ffffd1022d000000

    Number of elements 0x080
    Owned by OS        0x080
    Owned by Client    00000

    Begin Index        0x078 (ffffd1022d003c40 - NET_PACKET)
    Next Index         0x078 (ffffd1022d003c40 - NET_PACKET)
    End Index          0x078 (ffffd1022d003c40 - NET_PACKET)

    List all elements
```

このネットワークを表示する\_リング\_バッファーの要素、クリックするか"List のすべての要素"の詳細 の下部にあるリンクまたは入力、 **! ndiskd.netrb-ダンプ**コマンドラインでコマンド。 次の例を簡潔にするための excised 中間要素としました。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_リング\_バッファー](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-ring-buffer)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

 

 






