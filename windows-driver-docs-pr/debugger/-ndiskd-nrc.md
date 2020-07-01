---
title: ndiskd nrc
description: Ndiskd nrc 拡張機能には、NET_PACKET_FRAGMENT 構造に関する情報が表示されます。
ms.assetid: 366851FC-98B5-4322-AEDF-DBA20AA4FC9F
keywords:
- ndiskd nrc Windows デバッグ
ms.date: 06/17/2020
topic_type:
- apiref
api_name:
- ndiskd.nrc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f24efd18d84aea9d560c58fc2ea695adcff3b487
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85600940"
---
# <a name="ndiskdnrc"></a>! ndiskd nrc

**! Ndiskd nrc**拡張機能には、 [NET \_ RING \_ コレクション](https://docs.microsoft.com/windows-hardware/drivers/ddi/ringcollection/ns-ringcollection-_net_ring_collection)構造に関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx) 」および「 [Net リングの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/introduction-to-net-rings)」を参照してください。

```console
!ndiskd.nrc -handle <x> [-basic] [-packet] [-fragment] [-dump]
```

## <a name="parameters"></a>パラメーター

*-ハンドル*    
必須。 NET \_ RING コレクションの \_ アドレス

*-基本*    
パケットリングとフラグメントリングのリンクを表示します。

*-パケット*     
パケットリングの内容のみを表示します。

*-fragment*     
フラグメントリングの内容のみを表示します。

*-ダンプ*     
各要素 (パケット/フラグメント) に関する情報を表示します。

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
6. データパスキューのリングバッファーのハンドルをクリックします。 未定-これは nrc で動作しますか?
7. リングバッファーの詳細の下部にある [すべての要素の一覧表示] リンクをクリックして、含まれている要素を確認します。 未定の未定
8. いずれかの NET \_ RING コレクションオブジェクトをクリックし \_ ます。

この手順の手順1-4 の詳細については、 **! ndiskd cxadapter**トピックの例を参照してください。 この手順の手順5の詳細については、 [**! ndiskd netqueue**](-ndiskd-netqueue.md)のトピックの例を参照してください。 この手順の手順6-7 の詳細については、 [**「」の**](-ndiskd-netrb.md)例を参照してください。

次の例では、このネットリングコレクションの ffffffTBDffffffffff のハンドルを \_ 探し \_ ます。

```console
0: kd> !ndiskd.nrc ffffffTBDffffffffff


TBD

TBD

TBD

```

この例では、-packet オプションの使用を示していますが、未定と表示されています。

```console
0: kd> !ndiskd.nrc ffffffTBDffffffffff -packet

TBD

TBD

TBD

```

この例では、-fragment (または dump) の使用方法を示しています。 未定) オプションを選択して、未定と表示します。

```console
0: kd> !ndiskd.nrc ffffffTBDffffffffff -fragment

TBD

TBD

TBD

```

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワークアダプターの WDF クラス拡張 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET \_ RING \_ コレクション](https://docs.microsoft.com/windows-hardware/drivers/ddi/ringcollection/ns-ringcollection-_net_ring_collection)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

[**!ndiskd.netpacket**](-ndiskd-netpacket.md)
