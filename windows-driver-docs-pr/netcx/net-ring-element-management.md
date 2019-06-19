---
title: Net リング要素の管理
description: 2 つのロールを USB コント ローラーは、Windows、Windows 10 以降ではサポートされています。
ms.date: 06/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 030ba41a3f62f31c24b7fe66808089eb6d3e0aed
ms.sourcegitcommit: 280ab1c75f30404c63d2c011549f7af16ad56f31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "67235840"
---
# <a name="net-ring-element-management"></a>Net リング要素の管理

管理するには、このトピックのガイダンスに従って、 [ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/ns-ring-_net_ring)構造体とその要素中にネットワーク データ転送。 ルールは、このトピックでは、net リング要素のクライアント ドライバーのメンバーを変更できるデータ パスのシナリオで、クライアント ドライバーの全般的な情報に応じて必要があることに注意してこれらの構造をについて説明します。 

> [!IMPORTANT]
> クライアント ドライバーは、開発のすべてのフェーズ中に、次の手順に従う必要があります。 かどうか、クライアント ドライバーに準拠していない、次の手順でのテスト中に[Driver Verifier](../devtest/driver-verifier.md)、Driver Verifier は、違反を報告し、テスト対象のデバイスでのバグ チェックを実行します。

## <a name="netring"></a>NET_RING

ときに、 [ **NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/ns-ring-_net_ring)の親のパケットのキューを開始に、リング内のすべてのインデックスが初期化されます**0**します。

次の表では、net のどのメンバーがそのクライアント ドライバーを変更できますをリングについて説明します。

| フィールド | クライアント ドライバーが変更を許可します。 |
| --- | --- |
| OSReserved1 | X |
| ElementStride | X |
| numberOfElements | X |
| ElementIndexMask | X |
| EndIndex | X |
| OSReserved0 | X |
| OSReserved2 | X |
| BeginIndex | [はい] (必須) |
| NextIndex | [はい] (省略可能)**注**:フレームワークが読み取られません**NextIndex**します。 |
| スクラッチ | [はい] (省略可能)**注**:フレームワークが読み取られません**スクラッチ**します。 |
| バッファー | X |

クライアント ドライバーは、読み取りのみ、この構造体のメンバーを変更する必要がありますもする必要があります、これまでインクリメント**BeginIndex**過去**EndIndex**への呼び出し中に[ *EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)します。

Net のリング内のインデックスの所有権の詳細については、次を参照してください。[リングと net リングを行う反復子を Net](net-rings-and-net-ring-iterators.md)します。

## <a name="netpacket"></a>NET_PACKET

内のフィールドを[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/ns-packet-_net_packet)は、データ パスが動作する別のコンテキストに影響します。 かどうか、パケットの**無視**フィールドはセットであり、ドライバーが (Rx) を受信するかどうか、またはパケット (テキサス州) の送信パケットに適用されるルール セットを変更します。

次の表に、各シナリオでのドライバーの方法について説明します。

| 送受信 | 無視フィールドを設定しています. | メモ |
| --- | --- | --- |
| Rx | クライアント ドライバー | <ul><li>Rx では、中にクライアント ドライバーが設定**無視**必要に応じて、およびフレームワークによって読み取られる場合。 クライアント ドライバーは、読み取る必要はありません**無視**Rx の任意の時点。</li><li>クライアント ドライバーが設定されている場合、**無視**Rx の中にフィールド。<ul><li>クライアント ドライバーに書き込む必要があります、**無視**ハードウェアを正常に割り当てられていないパケットの受信操作をキャンセルする場合のフィールドします。 詳細については、次を参照してください。 [net リングとネットワーク データをキャンセル](canceling-network-data-with-net-rings.md)します。</li><li>クライアント ドライバー関連付ける必要がありますいないリソース パケット解放されないためです。</li></ul></li><li>クライアント ドライバーが設定されていない場合、**無視**Rx の中にフィールド。<ul><li>クライアント ドライバーを設定する必要があります**FragmentIndex**、 **FragmentCount**、およびすべてのフィールドに**レイアウト**します。</li><li>**FragmentIndex**間である必要があります**BeginIndex**包括と**EndIndex**フラグメント リングに排他的です。</li><li>**FragmentCount**間フラグメントの数を超えることはできません**BeginIndex**包括的と**EndIndex**フラグメント リングに排他的です。</li><li>クライアント ドライバーは、パケットのリングを移動する必要があります**BeginIndex** 、対応するフラグメントのリングを移動した場合**BeginIndex**します。</li><li>呼び出し後[ *EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)クライアント ドライバーがパケットのリングをインクリメントする場合、 **BeginIndex**ドライバーでは、フラグメント リングを増やす必要がありますも、**BeginIndex**過去のパケットのフラグメント。 フラグメント リングつまり**BeginIndex**に移動する必要があります、 **EndIndex**の前のパケットのフラグメント。</li></ul></ul> |
| テキサス州 | NetAdapterCx | <ul><li>クライアント ドライバー以外のすべてのパケット内のフィールドは変更しないで**スクラッチ**します。</li><li>クライアント ドライバーでの値を読み取ることができます**無視**書き込む必要があることはありません。</li><li>ドライバーする必要がありますの可能性があります以外の任意のフィールドを読み取れません Tx パケットが無視される場合は**スクラッチ**、必要な場合。</li></ul> |

### <a name="netpacketlayout"></a>NET_PACKET_LAYOUT

Rx の操作中に、**レイアウト**のフィールド、 [ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/ns-packet-_net_packet)次のルールが適用されます。

- フィールドを除くすべて**Reserved0**クライアント ドライバーで初期化する必要があります。
- 場合**Layer2Type**に設定されている**NetPacketLayer2TypeEthernet**、し**Layer2HeaderLength**あります**14**以上。
- 場合**Layer2Type**に設定されている**NetPacketLayer2TypeNull**、し**Layer2HeaderLength**に設定する必要があります**0**します。
- 場合**Layer3Type**は IPv4 の種類、 **Layer3HeaderLength**必要があります**20**以上。
- 場合**Layer3Type**し、IPv6 の種類は、 **Layer3HeaderLength**必要があります**40**以上。
- 場合**Layer4Type**に設定されている**Tcp**、し**Layer4HeaderLength**あります**40**以上。
- 場合**Layer4Type**に設定されている**Udp**、し**Layer4HeaderLength**あります**8**以上。
- レイヤーの種類のフィールドは、適切な列挙型の範囲内にする必要があります。

**レイアウト**Tx 中には使用されません。

## <a name="netfragment"></a>NET_FRAGMENT

[**NET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fragment/ns-fragment-_net_fragment)フィールド規則は、ドライバーを受信または送信するかどうかとドライバーによって、またはフレームワークによって、パケットに関連付けられたフラグメント バッファーのかどうかによって異なります。

| 送受信 | メモ |
| --- | --- |
| Rx | <ul><li>クライアント ドライバーが書き込むことはできません、 **OsReserved_Bounced**フィールド。</li><li>ドライバーがない接続し、場合**容量**は変更できませんが、 **ValidLength**と**オフセット**変更する必要があります。</li><li>ドライバーは、アタッチする場合**容量**、 **ValidLength**、および**オフセット**すべてを変更する必要があります。</li><li>**オフセット** + **ValidLength**必要がありますより小さい**容量**します。</li></ul> |
| テキサス州 | <ul><li>クライアント ドライバーは、以外のすべてのフィールドを変更できません**スクラッチ**します。</li></ul> |