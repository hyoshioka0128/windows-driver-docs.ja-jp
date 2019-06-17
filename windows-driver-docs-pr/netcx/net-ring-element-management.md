---
title: Net リング要素の管理
description: 2 つのロールを USB コント ローラーは、Windows、Windows 10 以降ではサポートされています。
ms.date: 06/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3fbe601e67fed2d7f30c3afb3ac13d8dced57582
ms.sourcegitcommit: 91b989fc3256267fab89c36b1fa54ff039dcc687
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148818"
---
# <a name="net-ring-element-management"></a>Net リング要素の管理

NetAdapterCx クライアント ドライバーをテストするときに[Driver Verifier](../devtest/driver-verifier.md)、管理するには、このトピックのガイダンスに従って、 [ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/ns-ring-_net_ring)構造とその要素。 ルールは、このトピックでは、net リング要素のクライアント ドライバーのメンバーを変更できるデータ パスのシナリオで、クライアント ドライバーの全般的な情報に応じて必要があることに注意してこれらの構造をについて説明します。 クライアント ドライバーは、次の手順に準拠していない、Driver Verifier は違反を報告し、テスト対象のデバイスでのバグ チェックを実行します。

## <a name="netring"></a>NET_RING

ときに、 [ **NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/ns-ring-_net_ring)の親のパケットのキューを開始に、リング内のすべてのインデックスが初期化されます**0**します。

次の表では、net のどのメンバーがそのクライアント ドライバーを変更できますをリングについて説明します。

| フィールド | クライアント ドライバーが変更を許可します。 | 必要なまたは変更する (省略可能) | 
| --- | --- | --- |
| OSReserved1 | X | なし  |
| ElementStride | X | なし |
| numberOfElements | X | なし |
| ElementIndexMask | X | なし |
| EndIndex | X | なし |
| OSReserved0 | X | なし |
| OSReserved2 | X | なし |
| BeginIndex | 〇 | 必須 |
| NextIndex | 〇 | 省略可能 |
| スクラッチ | 〇 | 省略可能 |
| バッファー | X | なし |

Driver Verifier は、net のリングで、次のいずれかが発生した場合、違反を報告します。

- 場合**BeginIndex** \> **EndIndex**
- 任意の読み取り専用フィールドが変更された場合

フレームワークが読み取られません**NextIndex**または**スクラッチ**します。

## <a name="netpacket"></a>NET_PACKET

内のフィールドを[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/ns-packet-_net_packet)は、データ パスが動作する別のコンテキストに影響します。 かどうか、パケットの**無視**フィールドはセットであり、ドライバーが (Rx) を受信するかどうか、またはパケット (テキサス州) の送信パケットに適用されるルール セットを変更します。

次の表に、各シナリオでのドライバーの方法について説明します。

| 送受信 | フィールド セットを無視します。 | メモ |
| --- | --- | --- |
| Rx | 〇 | <ul><li>読み取るクライアント ドライバーの意味のある方法はありません、**無視**Rx の中にフィールド。</li><li>クライアント ドライバーに書き込む必要があります、**無視**Rx の操作をキャンセルする場合のフィールドします。</li><li>場合**無視**設定は、Rx では、中に、フレームワークは読み取らない場合その他のフィールド。 そのため、クライアント ドライバー関連付ける必要がありますいないリソース パケット解放されないためです。</li></ul> |
| Rx | X | <ul><li>クライアント ドライバーを設定する必要があります**FragmentIndex**、 **FragmentCount**、およびすべてのフィールドに**レイアウト**します。</li><li>**FragmentIndex**間である必要があります**BeginIndex**包括と**EndIndex**フラグメント リングに排他的です。</li><li>**FragmentCount**間フラグメントの数を超えることはできません**BeginIndex**包括的と**EndIndex**フラグメント リングに排他的です。</li><li>Driver Verifier は、クライアント ドライバーは、フラグメントを移動する場合に違反を報告**BeginIndex**パケットではありませんが、 **BeginIndex**します。</li><li>呼び出し後[ *EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)クライアント ドライバーがパケットのリングをインクリメントする場合、 **BeginIndex**ドライバーでは、フラグメント リングを増やす必要がありますも、**BeginIndex**過去のパケットのフラグメント。 フラグメント リングつまり**BeginIndex**に移動する必要があります、 **EndIndex**の前のパケットのフラグメント。</li></ul> |
| テキサス州 | どちらもオン | <ul><li>クライアント ドライバー以外のすべてのパケット内のフィールドは変更しないで**スクラッチ**します。</li></ul> |
| テキサス州 | 〇 | <ul><li>クライアント ドライバーでの値を読み取ることができます**無視**書き込む必要があることはありません。</li><li>ドライバーする必要がありますの可能性があります以外の任意のフィールドを読み取れません Tx パケットが無視される場合は**スクラッチ**、必要な場合。</li></ul> |

### <a name="netpacketlayout"></a>NET_PACKET_LAYOUT

**レイアウト**のフィールド、 [ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/ns-packet-_net_packet)次のルールが適用されます。

- フィールドを除くすべて**Reserved0**クライアント ドライバーで初期化する必要があります。
- 場合**Layer2Type**に設定されている**NetPacketLayer2TypeEthernet**、し**Layer2HeaderLength**あります**14**以上。
- 場合**Layer2Type**に設定されている**NetPacketLayer2TypeNull**、し**Layer2HeaderLength**に設定する必要があります**0**します。
- 場合**Layer3Type**は IPv4 の種類、 **Layer3HeaderLength**必要があります**20**以上。
- 場合**Layer3Type**し、IPv6 の種類は、 **Layer3HeaderLength**必要があります**40**以上。
- 場合**Layer4Type**に設定されている**Tcp**、し**Layer4HeaderLength**あります**40**以上。
- 場合**Layer4Type**に設定されている**Udp**、し**Layer4HeaderLength**あります**8**以上。
- レイヤーの種類のフィールドは、適切な列挙型の範囲内にする必要があります。

## <a name="netfragment"></a>NET_FRAGMENT

[**NET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fragment/ns-fragment-_net_fragment)フィールド規則は、ドライバーを受信または送信するかどうかとドライバーによって、またはフレームワークによって、パケットに関連付けられたフラグメント バッファーのかどうかによって異なります。

| 送受信 | メモ |
| --- | --- |
| Rx | <ul><li>クライアント ドライバーが書き込むことはできません、 **OsReserved_Bounced**フィールド。</li><li>ドライバーの場合*いない*アタッチし、**容量**は変更できませんが、 **ValidLength**と**オフセット**変更する必要があります。</li><li>場合、ドライバー*は*アタッチし、**容量**、 **ValidLength**、および**オフセット**すべてを変更する必要があります。</li><li>**オフセット**必要がありますより小さい**ValidLength**します。</li><li>**ValidLength**必要がありますより小さい**容量。**
| テキサス州 | <ul><li>クライアント ドライバーは、以外のすべてのフィールドを変更できません**スクラッチ**します。</li></ul> |