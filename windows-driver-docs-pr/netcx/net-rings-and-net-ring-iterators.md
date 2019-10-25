---
title: ネット リングとネット リングの反復子の概要
description: このトピックでは、ネットワークリングと net リング反復子について説明します。
ms.assetid: 8A56AA21-264C-4C1A-887E-92C9071E8AB8
keywords:
- NetAdapterCx net リングと net ring 反復子の概要、NetCx のネットリングと net ring 反復子の概要、NetAdapterCx PCI デバイスの net ring、NetAdapterCx 非同期 i/o
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7ece878b12451d110a9f247e36ba654b3fde28b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835524"
---
# <a name="introduction-to-net-rings-and-net-ring-iterators"></a>ネット リングとネット リングの反復子の概要

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

## <a name="net_ring-overview"></a>NET_RING の概要

**NET_RING**は、NetAdapterCx とクライアントドライバー間で共有されるネットワークデータの循環バッファーです。 クライアントドライバーのすべてのパケットキューには、コアパケット記述子用の*パケットリング*と、各パケットのフラグメント記述子の*フラグメントリング*という2つのリングがあります。

パケット記述子の詳細については、「[パケット記述子と拡張機能](packet-descriptors-and-extensions.md)」を参照してください。

パケットリング内のすべてのコア記述子は、そのパケットのフラグメント記述子を特定するためにフラグメントリングにインデックスを持ちます。 もう1つのデータ構造である**NET_RING_COLLECTION**は、次の図に示すように、特定のパケットキューに対してパケットリングとフラグメントリングをまとめてグループ化します。

![マルチリングレイアウト](images/multi-ring.png) 

各パケットキューには、独自の**NET_RING_COLLECTION**構造体があります。その結果、独自のパケットリング、フラグメントリング、およびそれらのリングの記述子があります。 このため、各パケットキューのネットワークデータ転送操作は完全に独立しています。 パケットキューの詳細については、「[キューの送信と受信](transmit-and-receive-queues.md)」を参照してください。

## <a name="net_ring-element-ownership"></a>NET_RING 要素の所有権

**NET_RING**内の各要素は、クライアントドライバーまたは NetAdapterCx のいずれかによって所有されています。 所有権は、 **NET_RING**のセクションをマークする3つのインデックスによって制御されます。 これらのインデックスについては、次の表で説明します。 これらのインデックスを移動する操作 (クライアントドライバーが[Net Ring 反復子インターフェイス](#net-ring-iterator-interface-overview)を呼び出すことによって行われる処理) は、 *post*と*ドレイン*のセマンティクスによって記述されます。 

| **NET_RING**インデックス名 | 説明 | ネットワークデータの転送に必要 | ［更新者］ |
| --- | --- | --- | --- |
| BeginIndex | NIC クライアントドライバーが所有する**NET_RING**内の要素の範囲の先頭。 **Beginindex**は、 **NET_RING**の*ドレイン*セクションの先頭でもあります。 **Beginindex**がインクリメントされると、ドライバーはリングから要素を*ドレイン*し、その所有権を OS に転送します。 | [はい] | NIC クライアントドライバー (Net Ring 反復子インターフェイス API 呼び出しを使用) |
| NextIndex | **NET_RING**の*post*セクションの先頭。 **Nextindex**は、クライアントドライバーが所有するリングのセクションを、post およびドレインサブセクションに分割します。 **Nextindex**がインクリメントされると、ドライバーはバッファーをハードウェアに*ポスト*し、バッファーをリングのドレインセクションに転送します。 | 必須ではない | NIC クライアントドライバー (Net Ring 反復子インターフェイス API 呼び出しを使用) |
| EndIndex | NIC クライアントドライバーが所有する**NET_RING**内の要素の範囲の末尾。 クライアントドライバーは **、EndIndex**を含む要素を所有します。 | [はい] | NetAdapterCx |

パケットキューの[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)コールバック中に、これらのインデックスを net ring 反復子で操作することは、クライアントドライバーがシステムとネットワークインターフェイスカード (NIC) ハードウェアの間でネットワークデータを転送する方法です。

クライアントドライバーは、 **Beginindex**から**EndIndex**へのすべての要素を所有します。 たとえば、 **Beginindex**が2で**EndIndex**が5の場合、クライアントドライバーは、インデックス値が2、3、および4の要素の3つの要素を所有します。

**Beginindex**が**EndIndex**と等しい場合、クライアントドライバーは要素を所有していません。

NetAdapterCx は、 **EndIndex**をインクリメントして、要素をリングバッファーにポストします。 クライアントドライバーは、リングのドレイン反復子を進めることで、バッファーをドレインし、要素の所有権を返します。これにより、 **Beginindex**がインクリメントされます。

**Nextindex**は、クライアントドライバーが使用する場合は省略可能であり、リングのクライアントドライバーのセクションの post サブセクションとドレインサブセクションを分離するために用意されています。

**Nextindex**と**EndIndex**の間のインデックス値を含む要素は、クライアントによって所有されていますが、まだハードウェアにポストされていません。 **Nextindex**が**beginindex**と等しい場合、クライアントドライバーには、OS に転送するための完了したバッファーがありません。 **Nextindex**が**EndIndex**と等しい場合、クライアントドライバーにはハードウェアに post するバッファーがありません。

ネットワークリングは循環しているため、最終的にはインデックス値がバッファーの末尾をラップし、先頭に戻ります。 NetAdapterCx は、次のセクションで説明するように、クライアントドライバーが適切なメソッドを呼び出すと、リングの周りのインデックス値のラップを自動的に処理します。

ネットワークリングの要素の管理に関する具体的な情報については、「 [net ring 要素の管理](net-ring-element-management.md)」を参照してください。

## <a name="net-ring-iterator-interface-overview"></a>Net Ring 反復子インターフェイスの概要

NIC クライアントドライバーは、 *Net Ring 反復子インターフェイス*を呼び出すことによって、ネットリングに対して post およびドレイン操作を実行します。 [**NET_RING_ITERATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/ns-netringiterator-_net-ring-iterator)は、所属する**NET_RING**の post およびドレインインデックスへの参照を含む小さな構造です。 

各**NET_RING**には複数の反復子を含めることができます。 たとえば、パケットリングには、リングのドレインセクション (*ドレイン反復子*)、リングの post セクション (*ポスト反復*子) をカバーする反復子、および post セクションとドレインセクションの両方をカバーする反復子があります。 同様に、フラグメントリングは同じ反復子を持つことができます。

クライアントドライバーが各リングの各反復子を簡単に制御できるようにするため、Net Ring 反復子インターフェイスは反復子を[**NET_RING_PACKET_ITERATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/ns-netringiterator-_net-ring-packet-iterator)と[**NET_RING_FRAGMENT_ITERATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/ns-netringiterator-_net-ring-fragment-iterator)の2つのカテゴリに分けます。 これらは**NET_RING_ITERATOR**のラッパー構造であり、すべての NET RING 反復子インターフェイスの呼び出しで使用されます。 クライアントドライバーは、 **NET_RING_ITERATOR**を直接使用することはできません。 代わりに、特定のネットリング (パケットまたはフラグメント) に対して適切な反復子を使用する必要があります。

クライアントドライバーは、net ring 反復子を取得、昇格、および設定することによって、パケットキュー内のネットワークデータを送受信します。 クライアントドライバーは、リングの要素にアクセスするために、net ring 反復子のメソッドも呼び出します。

Net ring 反復子のデータ構造体とメソッドの完全な一覧については、「 [Netringiterator. h](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/)」を参照してください。

## <a name="sending-and-receiving-network-data-with-net-rings-and-net-ring-iterators"></a>ネットワークリングと net ring 反復子を使用したネットワークデータの送受信

ネットワークデータをネットリングで送信および受信する方法の詳細とコードサンプルについては、次のトピックを参照してください。

[ネットワークリングを使用したネットワークデータの送信](sending-network-data-with-net-rings.md)

[ネットワークリングを使用したネットワークデータの受信](receiving-network-data-with-net-rings.md)
