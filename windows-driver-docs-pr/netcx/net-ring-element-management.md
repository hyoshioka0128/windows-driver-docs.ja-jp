---
title: Net ring 要素の管理
description: Windows では、Windows 10 以降で USB デュアルロールコントローラーがサポートされるようになりました。
ms.date: 06/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: cc0aa0f00eb41358c37bb7cffc95be022d47e6f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838273"
---
# <a name="net-ring-element-management"></a>Net ring 要素の管理

ネットワークデータ転送中に[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)構造とその要素を管理するには、このトピックのガイダンスに従ってください。 このトピックでは、クライアントドライバーが変更できる net ring 要素のメンバーと、データパスのシナリオによっては、これらの構造に関する一般的な情報について説明します。 

> [!IMPORTANT]
> クライアントドライバーは、開発のすべてのフェーズでこれらの指示に従う必要があります。 [ドライバー検証ツール](../devtest/driver-verifier.md)を使用したテスト中にクライアントドライバーがこれらの指示に従わない場合、ドライバーの検証ツールは違反を報告し、テスト対象のデバイスでバグチェックをトリガーします。

## <a name="net_ring"></a>NET_RING

[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)の親パケットキューが開始されると、リング内のすべてのインデックスが**0**に初期化されます。

次の表では、クライアントドライバーが変更できるネットワークリングのメンバーについて説明します。

| フィールド | クライアントドライバーの変更が許可されています |
| --- | --- |
| OSReserved1 | いいえ |
| ElementStride | いいえ |
| NumberOfElements | いいえ |
| ElementIndexMask | いいえ |
| EndIndex | いいえ |
| OSReserved0 | いいえ |
| OSReserved2 | いいえ |
| BeginIndex | はい (必須) |
| NextIndex | はい (省略可能) 注: フレームワークは**Nextindex**を読み取らないことに**注意**してください。 |
| プラン | はい (省略可能)**メモ**: フレームワークは**スクラッチ**を読み取りません。 |
| Buffer | いいえ |

クライアントドライバーは、この構造の読み取り専用メンバーを変更することはできません。また、 [*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)の呼び出し中に、 **Beginindex**を**EndIndex**よりも大きくする必要はありません。

ネットリングでのインデックスの所有権の詳細については、「 [net リングと net ring 反復子](net-rings-and-net-ring-iterators.md)」を参照してください。

## <a name="net_packet"></a>NET_PACKET

[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet)のフィールドは、データパスが動作するさまざまなコンテキストに依存します。 パケットの **[無視]** フィールドが設定されているかどうか、およびドライバーが受信 (Rx) または送信 (Tx) のどちらであるかにかかわらず、パケットに適用されているルールセットが変更されます。

次の表では、各シナリオでのドライバーの手順について説明します。

| Rx または Tx | 無視フィールドはによって設定されています... | 説明 |
| --- | --- | --- |
| Rx | クライアントドライバー | <ul><li>Rx 中、クライアントドライバーは必要に応じて**無視**し、フレームワークはそれを読み取ります。 クライアントドライバーは、Rx 中のどの時点でも**無視**を読み取る必要はありません。</li><li>クライアントドライバーが Rx 中に**無視**フィールドを設定した場合、次のようになります。<ul><li>ハードウェアに対して正常にプログラミングされていないパケットに対して Rx 操作をキャンセルする場合、クライアントドライバーは**無視**フィールドに書き込む必要があります。 詳細については、「 [net リングを使用したネットワークデータのキャンセル](canceling-network-data-with-net-rings.md)」を参照してください。</li><li>クライアントドライバーは解放されないため、リソースをパケットに関連付けることはできません。</li></ul></li><li>Rx 中にクライアントドライバーが**無視**フィールドを設定しない場合は、次のようになります。<ul><li>クライアントドライバーは、 **Fragmentindex**、 **fragmentindex**、および**Layout**のすべてのフィールドにデータを設定する必要があります。</li><li>**Fragmentindex**は、フラグメントリング内の**Beginindex**と**EndIndex** exclusive の間でなければなりません。</li><li>**Fragmentcount**は、フラグメントリング内の**beginindex**包括と**EndIndex** exclusive の間のフラグメントの数を超えることはできません。</li><li>クライアントドライバーが対応するフラグメントリング**Beginindex**を移動する場合は、パケットリング**beginindex**を移動する必要があります。</li><li>[*Evtpacketqueueadvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)を呼び出した後、クライアントドライバーがパケットリング**beginindex**をインクリメントした場合、ドライバーは、そのパケットのフラグメントを超えたフラグメントリング**beginindex**もインクリメントする必要があります。 言い換えると、フラグメントリングの**Beginindex**は、前のパケットのフラグメントの**EndIndex**に移動します。</li></ul></ul> |
| トランザクション | NetAdapterCx | <ul><li>クライアントドライバーは、**ゼロ**以外のすべてのパケット内のフィールドを変更することはできません。</li><li>クライアントドライバーは、 **[無視]** の値を読み取ることができますが、書き込むことはできません。</li><li>Tx パケットが無視された場合は、必要に応じて、ドライバーが**ゼロ**以外のフィールドを読み取る必要はありません。</li></ul> |

### <a name="net_packet_layout"></a>NET_PACKET_LAYOUT

Rx 操作中、 [**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet)の**Layout**フィールドには次の規則が適用されます。

- **Reserved0**を除くすべてのフィールドは、クライアントドライバーで初期化する必要があります。
- **Layer2Type**が**NetPacketLayer2TypeEthernet**に設定されている場合、 **Layer2HeaderLength**は**14**以上である必要があります。
- **Layer2Type**が**NetPacketLayer2TypeNull**に設定されている場合は、 **Layer2HeaderLength**を**0**に設定する必要があります。
- **Layer3Type**が IPv4 型の場合、 **Layer3HeaderLength**は**20**以上である必要があります。
- **Layer3Type**が IPv6 の種類である場合、 **Layer3HeaderLength**は**40**以上である必要があります。
- **Layer4Type**が**Tcp**に設定されている場合、 **Layer4HeaderLength**は**40**以上である必要があります。
- **Layer4Type**が**Udp**に設定されている場合、 **Layer4HeaderLength**は**8**以上である必要があります。
- レイヤーの種類のフィールドは、適切な列挙範囲内にある必要があります。

**レイアウト**は、Tx 中には使用されません。

## <a name="net_fragment"></a>NET_FRAGMENT

[**NET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fragment/ns-fragment-_net_fragment)フィールドの規則は、ドライバーが受信または送信しているかどうか、およびフラグメントバッファーがドライバーまたはフレームワークによってパケットにアタッチされているかどうかによって異なります。

| Rx または Tx | 説明 |
| --- | --- |
| Rx | <ul><li>クライアントドライバーは、 **OsReserved_Bounced**フィールドに書き込むことができません。</li><li>ドライバーがアタッチされていない場合、**容量**を変更する必要はありませんが、 **Validlength**と**Offset**を変更する必要があります。</li><li>ドライバーがアタッチされている場合は、**容量**、 **validlength**、および**Offset**がすべて変更されている必要があります。</li><li> + **Validlength**の**オフセット**には**容量**よりも小さい値を指定する必要があります。</li></ul> |
| トランザクション | <ul><li>クライアントドライバーは、**ゼロ**以外のフィールドを変更することはできません。</li></ul> |