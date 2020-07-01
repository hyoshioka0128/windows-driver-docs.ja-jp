---
title: ndiskd netring
description: この拡張機能には、NET_PACKET_FRAGMENT 構造に関する情報が表示されます。
ms.assetid: 342AFF9B-2DC2-4650-8787-DEC70753ABDE
keywords:
- ndiskd Windows デバッグの終了
ms.date: 06/17/2020
topic_type:
- apiref
api_name:
- ndiskd.netring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86533586029cc633d0cdf873862389060ba7e720
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85600942"
---
# <a name="ndiskdnetring"></a>ndiskd netring

この**拡張機能には**、 [NET \_ RING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)構造体に関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx) 」および「 [Net リングの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/introduction-to-net-rings)」を参照してください。

```console
!ndiskd.netring -handle <x> [-basic] [-dump]
```

## <a name="parameters"></a>パラメーター

*-ハンドル*   
必須。 NET_RING のアドレス

*-基本*    
基本情報を表示します

*-ダンプ*    
各要素に関する情報を表示します。

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
6. データパスキューのリングバッファーのハンドルをクリックします。 未定-これは netring と連携しますか。
7. リングバッファーの詳細の下部にある [すべての要素の一覧表示] リンクをクリックして、含まれている要素を確認します。 未定の未定
8. NET \_ RING (Collection?) オブジェクトの1つをクリックします。
この手順の手順1-4 の詳細については、 **! ndiskd cxadapter**トピックの例を参照してください。 この手順の手順5の詳細については、 [**! ndiskd netqueue**](-ndiskd-netqueue.md)のトピックの例を参照してください。 この手順の手順6-7 の詳細については、 [**「」の**](-ndiskd-netrb.md)例を参照してください。 未定  

次の例では、 [**! ndiskd cxadapter**](-ndiskd-cxadapter.md)拡張機能を使用して、未定となることを確認します。

```console
0: kd> !ndiskd.cxdapter 

TBD

TBD

TBD


```

未定のアドレスを使用して、netring を表示します。

```console
0: kd> !ndiskd.netring ffffTBDfffff

TBD

TBD

TBD


```

この例では、-dump オプションを使用して、各要素に関する情報を表示する方法を示します。

```console
0: kd> !ndiskd.netring ffffTBDfffff -dump

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

[NET \_ RING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

[**!ndiskd.netpacket**](-ndiskd-netpacket.md)
