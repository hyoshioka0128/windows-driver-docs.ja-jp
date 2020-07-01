---
title: ndiskd netfragment
description: Ndiskd netfragment 拡張機能には、NET_PACKET_FRAGMENT 構造に関する情報が表示されます。
ms.assetid: 2075D682-45F5-414D-A8ED-0494B3550C77
keywords:
- ndiskd netfragment Windows デバッグ
ms.date: 06/17/2020
topic_type:
- apiref
api_name:
- ndiskd.netfragment
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 72936bcd51fcece1f8191b16c346d52be0d1cf80
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85600944"
---
# <a name="ndiskdnetfragment"></a>! ndiskd netfragment

**! Ndiskd netfragment**拡張機能には、 [NET \_ パケット \_ フラグメント](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet-fragment)構造に関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)」を参照してください。

```console
!ndiskd.netfragment -handle <x> 
```

## <a name="parameters"></a>パラメーター

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 NET \_ パケットフラグメントのアドレス \_ 。

### <a name="dll"></a>[DLL]

Ndiskd.dll

### <a name="examples"></a>例

**メモ**   「[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)」を参照して、NET \_ PACKET オブジェクトと NetAdapterCx 内の他のオブジェクトとの関係を説明する図を参照してください。

ネットパケットのハンドルを取得するには \_ 、次の手順を実行します。

1. [**! Ndiskd netadapter**](-ndiskd-netadapter.md)拡張機能を実行します。
2. NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3. NetAdapter の NETADAPTER オブジェクトの右側にある [詳細情報] リンクをクリックして、 [**! ndiskd cxadapter**](-ndiskd-cxadapter.md)拡張機能を実行します。
4. *-データパス*パラメーターを指定して **! ndiskd cxadapter**コマンドを入力すると、netadapter のデータパスキューが表示されます。
5. データパスキューのいずれかのハンドルをクリックします。
6. データパスキューのリングバッファーのハンドルをクリックします。
7. リングバッファーの詳細の下部にある [すべての要素の一覧表示] リンクをクリックして、含まれている要素を確認します。
8. リングバッファーの要素の一覧で、いずれかの[NET \_ PACKET](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)オブジェクトをクリックします。

この手順の手順1-4 の詳細については、 **! ndiskd cxadapter**トピックの例を参照してください。 この手順の手順5の詳細については、 [**! ndiskd netqueue**](-ndiskd-netqueue.md)のトピックの例を参照してください。 この手順の手順6-7 の詳細については、 [**「」の**](-ndiskd-netrb.md)例を参照してください。 この手順の手順8の詳細については、 [**! ndiskd netpacket**](-ndiskd-netpacket.md)のトピックの例を参照してください。
次の例では、このネットパケットの最初のフラグメントのハンドルである ffffd1022d000040 を探し \_ ます。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

最初のフラグメントのハンドルをクリックするか、コマンドラインで **! ndiskd netfragment-handle**コマンドを入力して、このネットワークパケットフラグメントの詳細を確認できます。これには、 \_ \_ 仮想アドレス、容量、およびフラグメントのネットパケットチェーン内の最後のパケットであるかどうかが含まれ \_ ます。

```console
0: kd> !ndiskd.netfragment ffffd1022d000040

    NET_PACKET_FRAGMENT ffffd1022d000040

    Virtual Address    ffffd102303e82f8
    Capacity           0n92
    Valid Length       0n34
    Offset             0n58

    Last packet of chain
```

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワークアダプターの WDF クラス拡張 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET \_ パケット \_ フラグメント](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet-fragment)

[NET \_ パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

[**!ndiskd.netpacket**](-ndiskd-netpacket.md)
