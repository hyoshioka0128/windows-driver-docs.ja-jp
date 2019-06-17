---
title: ネット リングとネット リングの反復子
description: このトピックでは、net のリングと net リングを行う反復子について説明します。
ms.assetid: 8A56AA21-264C-4C1A-887E-92C9071E8AB8
keywords:
- NetAdapterCx Net リングと net リングを行う反復子、NetCx Net リング、net のリングの反復子 NetAdapterCx PCI デバイス net リング、NetAdapterCx 非同期 I/O
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 09a8b659455e676e46b1c8ca3d5f3daa36b534ca
ms.sourcegitcommit: 91b989fc3256267fab89c36b1fa54ff039dcc687
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148532"
---
# <a name="net-rings-and-net-ring-iterators"></a>ネット リングとネット リングの反復子

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

## <a name="netring-overview"></a>NET_RING の概要

A **NET_RING** NetAdapterCx と、クライアント ドライバーとの間で共有されるネットワーク データの循環バッファーします。 クライアント ドライバーでのすべてのパケット キューが 2 つのリング:*パケット リング*core パケットの記述子を*フラグメント リング*各パケットのフラグメントの記述子。

パケットの記述子の詳細については、次を参照してください。[パケット記述子と拡張機能](packet-descriptors-and-extensions.md)します。

パケットのリング内のすべてのコア記述子が、そのパケットのフラグメントの記述子を検索するため、フラグメント リングへのインデックス。 別のデータ構造体、 **NET_RING_COLLECTION**、次の図に示すように、パケットのリングとフラグメント リング パケット キューの連携をグループ化します。

![複数のリングのレイアウト](images/multi-ring.png) 

すべてのパケットのキューには、独自**NET_RING_COLLECTION**構造、および、その結果、独自のパケット リング フラグメント リング、およびそれらのリング内の記述子。 そのため、各パケット キューのネットワーク データ転送操作では完全に独立してます。 パケット キューの詳細については、次を参照してください。[送信および受信キュー](transmit-and-receive-queues.md)します。

## <a name="netring-element-ownership"></a>NET_RING 要素の所有権

内の各要素を**NET_RING**クライアント ドライバーまたは NetAdapterCx のいずれかによって所有されています。 所有権がのセクションをマークする 3 つのインデックスによって制御される、 **NET_RING**します。 これらのインデックスは、次の表で説明します。 呼び出すにどのドライバーがクライアントには、これらのインデックスを移動する操作、 [Net リング反復子インターフェイス](#net-ring-iterator-interface-overview)、によって定義された*投稿*と*ドレイン*セマンティクスです。 

| **NET_RING**インデックス名 | 説明 | ネットワーク データを転送するために必要な | ［更新者］ |
| --- | --- | --- | --- |
| BeginIndex | 内の要素の範囲の先頭、 **NET_RING** NIC クライアント ドライバーが所有しています。 **BeginIndex**の先頭ではまた、*ドレイン*のセクション、 **NET_RING**します。 ときに**BeginIndex**が増分され、ドライバー*放電*OS にそれらのリングと転送の所有権の要素。 | 〇 | Net リング反復子インターフェイスの API 呼び出しを介して、NIC のクライアント ドライバー |
| NextIndex | 先頭、*投稿*のセクション、 **NET_RING**します。 **NextIndex**投稿、ドレインのサブセクションに、クライアント ドライバーが所有しているリングのセクションに分割します。 ときに**NextIndex**が増分され、ドライバー*投稿*ハードウェアと、リングのドレイン セクションへの転送、バッファーをバッファーします。 | X | Net リング反復子インターフェイスの API 呼び出しを介して、NIC のクライアント ドライバー |
| EndIndex | 内の要素の範囲の末尾、 **NET_RING** NIC クライアント ドライバーが所有しています。 クライアント ドライバーが最大の要素を所有**EndIndex - 1**包括的です。 | 〇 | NetAdapterCx |

パケット キューの中に、net のリングの反復子でこれらのインデックスを操作する[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバックは、クライアント ドライバーがシステムとネットワーク インターフェイスのネットワーク データを転送する方法カード (NIC) のハードウェア。

クライアント ドライバーからのすべての要素を所有する**BeginIndex**に**EndIndex - 1**包括的です。 たとえば場合、 **BeginIndex** 2 と**EndIndex**が 5 の場合、クライアント ドライバーは、3 つの要素を所有している。 2、3、および 4 のインデックス値を持つ要素。

場合**BeginIndex**と等しい**EndIndex**、クライアント ドライバーが任意の要素を所有していません。

NetAdapterCx 増分することで、リング バッファーに要素を投稿する**EndIndex**します。 クライアント ドライバーは、バッファーをドレインし、進めるリングのドレイン反復子をインクリメントすることで、要素の所有権を返します**BeginIndex**します。

**NextIndex**はクライアント ドライバーを使用する省略可能ですし、リングのクライアント ドライバーのセクションの post とドレインのサブセクションを分離しやすくするために提供されます。

要素のインデックス値を持つ**NextIndex**と**EndIndex - 1**包括的なクライアントによって所有されますが、ハードウェアに投稿されていません。 場合**NextIndex**と等しい**BeginIndex**、クライアント ドライバーには、OS への転送を完了したバッファーはありません。 場合**NextIndex**と等しい**EndIndex**、クライアント ドライバーには、ハードウェアに投稿するすべてのバッファーはありません。

Net のリングが循環のため、最終的にインデックス値はバッファーの末尾をラップし、先頭に戻っています。 NetAdapterCx では、次のセクションで説明したクライアント ドライバーは、適切なメソッドを呼び出す場合リング内のインデックス値をラッピングが自動的に処理します。

Net のリング内の要素を管理する詳細については、次を参照してください。[リング要素の管理を Net](net-ring-element-management.md)します。

## <a name="net-ring-iterator-interface-overview"></a>Net のリングの反復子インターフェイスの概要

NIC クライアント ドライバーは post を実行し、net リングでの操作をドレインを呼び出すことによって、 *Net リング反復子インターフェイス*します。 A [ **NET_RING_ITERATOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/ns-netringiterator-_net-ring-iterator)の投稿、ドレイン インデックスへの参照を格納する小さな構造体には、 **NET_RING**属しています。 

各**NET_RING**複数の反復子を持つことができます。 たとえば、パケットのリングは、リングのドレイン セクションをカバーする反復子がある (、*反復子をドレイン*)、リングの後のセクションをカバーする反復子 (、*反復子を投稿*)、および反復子投稿、ドレインの両方のセクションについて説明します。 同様に、フラグメントのリングでは、反復子と同じことができます。

各反復子の各リングを制御するためのクライアント ドライバーを簡単には、ネットの反復子インターフェイスのリングは反復子を 2 つのカテゴリに分割します。[**NET_RING_PACKET_ITERATOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/ns-netringiterator-_net-ring-packet-iterator)と[ **NET_RING_FRAGMENT_ITERATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/ns-netringiterator-_net-ring-fragment-iterator)します。 これらは、周囲のラッパーの構造体、 **NET_RING_ITERATOR**すべての Net リング反復子インターフェイスの API 呼び出しで使用されます。 クライアント ドライバーを使用する必要があります、 **NET_RING_ITERATOR**直接します。 代わりに、反復子の適切な型指定 net のリング (パケットまたはフラグメント) の使用する必要があります。

取得して、先行するには、net リング反復子の設定、クライアント ドライバーは、送信し、そのパケットのキューでネットワーク データを受信します。 クライアント ドライバーは、リングの要素にアクセスする net リング反復子にもメソッドを呼び出します。

Net リング反復子のデータ構造とメソッドの完全な一覧を参照してください。 [Netringiterator.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/)します。

## <a name="sending-and-receiving-network-data-with-net-rings-and-net-ring-iterators"></a>Net のリングと net リングを行う反復子のネットワーク データを送受信します。

Net のリングでネットワーク データを送信および受信しているに関する詳細情報とコードのサンプルについては、次のトピックを参照してください。

[Net のリングとネットワーク データを送信します。](sending-network-data-with-net-rings.md)

[Net のリングとネットワーク データの受信](receiving-network-data-with-net-rings.md)
