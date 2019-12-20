---
title: ネットリングの概要
description: このトピックでは、ネットワークリングについて説明します。
ms.assetid: 8A56AA21-264C-4C1A-887E-92C9071E8AB8
keywords:
- NetAdapterCx net リングの概要, NetCx のネットリングの概要, NetAdapterCx PCI デバイスの net ring, NetAdapterCx 非同期 i/o
ms.date: 10/29/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e4d7b4340fdce0cc9d59a1ff0d1efd7a77536806
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252075"
---
# <a name="introduction-to-net-rings"></a>ネットリングの概要

## <a name="net_ring-overview"></a>NET_RING の概要

**NET_RING**は、NetAdapterCx とクライアントドライバー間で共有されるネットワークデータの循環バッファーです。 クライアントドライバーのすべてのパケットキューには、コアパケット記述子用の*パケットリング*と、各パケットのフラグメント記述子の*フラグメントリング*という2つのリングがあります。

パケット記述子の詳細については、「[パケット記述子と拡張機能](packet-descriptors-and-extensions.md)」を参照してください。

パケットリング内のすべてのコア記述子は、そのパケットのフラグメント記述子を特定するためにフラグメントリングにインデックスを持ちます。 別のデータ構造 ( **NET_RING_COLLECTION**) は、次の図に示すように、特定のパケットキューのパケットリングとフラグメントリングをまとめてグループ化します。

![マルチリングレイアウト](images/multi-ring.png) 

各パケットキューには、独自の**NET_RING_COLLECTION**構造があります。その結果、独自のパケットリング、フラグメントリング、およびそのリング内の記述子があります。 このため、各パケットキューのネットワークデータ転送操作は完全に独立しています。 パケットキューの詳細については、「[キューの送信と受信](transmit-and-receive-queues.md)」を参照してください。

## <a name="net_ring-element-ownership"></a>NET_RING 要素の所有権

**NET_RING**内の各要素は、クライアントドライバーまたは NetAdapterCx のいずれかによって所有されます。 所有権は、 **NET_RING**のセクションをマークする3つのインデックスによって制御されます。 これらのインデックスについては、次の表で説明します。 これらのインデックスを移動する操作は、 *post*と*ドレイン*のセマンティクスによって記述されます。 

| **NET_RING**インデックス名 | 説明 | ネットワークデータの転送に必要 | ［更新者］ |
| --- | --- | --- | --- |
| BeginIndex | NIC クライアントドライバーによって所有されている**NET_RING**内の要素の範囲の先頭。 **Beginindex**は、 **NET_RING**の*ドレイン*サブセクションの先頭でもあります。 **Beginindex**がインクリメントされると、ドライバーはリングから要素を*ドレイン*し、その所有権を OS に転送します。 | [はい] | NIC クライアントドライバー |
| NextIndex | **NET_RING**の*post*サブセクションの先頭。 **Nextindex**は、クライアントドライバーが所有するリングのセクションを、post およびドレインサブセクションに分割します。 **Nextindex**がインクリメントされると、ドライバーはバッファーをハードウェアに*ポスト*し、バッファーをリングのドレインセクションに転送します。 | 必須ではない | NIC クライアントドライバー |
| EndIndex | NIC クライアントドライバーによって所有されている**NET_RING**内の要素の範囲の末尾。 クライアントドライバーは **、EndIndex**を含む要素を所有します。 | [はい] | NetAdapterCx |

パケットキューの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバック中にこれらのインデックスを操作すると、クライアントドライバーがシステムとネットワークインターフェイスカード (NIC) ハードウェアの間でネットワークデータを転送する方法が異なります。

クライアントドライバーは、 **Beginindex**から**EndIndex**へのすべての要素を所有します。 たとえば、 **Beginindex**が2で**EndIndex**が5の場合、クライアントドライバーは、インデックス値が2、3、および4の要素の3つの要素を所有します。

**Beginindex**が**EndIndex**と等しい場合、クライアントドライバーは要素を所有していません。

NetAdapterCx は、 **EndIndex**をインクリメントして、要素をリングバッファーにポストします。 クライアントドライバーは、 **Beginindex**を進めることで、バッファーをドレインし、要素の所有権を返します。

**Nextindex**は、クライアントドライバーが使用する場合は省略可能であり、リングのクライアントドライバーのセクションの post サブセクションとドレインサブセクションを分離するために用意されています。

**Nextindex**と**EndIndex**の間のインデックス値を含む要素は、クライアントによって所有されていますが、まだハードウェアにポストされていません。 **Nextindex**が**beginindex**と等しい場合、クライアントドライバーには、OS に転送するための完了したバッファーがありません。 **Nextindex**が**EndIndex**と等しい場合、クライアントドライバーにはハードウェアに post するバッファーがありません。

ネットワークリングは循環しているため、最終的にはインデックス値がバッファーの末尾をラップし、先頭に戻ります。 NetAdapterCx は、クライアントドライバーが適切なメソッドを呼び出すと、リングの周りのインデックス値のラップを自動的に処理します。

ネットワークリングの要素の管理に関する具体的な情報については、「 [net ring 要素の管理](net-ring-element-management.md)」を参照してください。

## <a name="sending-and-receiving-network-data-with-net-rings"></a>ネットワークリングを使用したネットワークデータの送受信

ネットワークデータをネットリングで送信および受信する方法の詳細とコードサンプルについては、次のトピックを参照してください。

[ネットワークリングを使用したネットワークデータの送信](sending-network-data-with-net-rings.md)

[ネットワークリングを使用したネットワークデータの受信](receiving-network-data-with-net-rings.md)
