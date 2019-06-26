---
title: チェックサム タスクのオフロード
description: チェックサム タスクのオフロード
ms.assetid: 5fb2f379-c357-4ec3-b103-bdbe23fcc033
keywords:
- タスクのオフロード WDK TCP/IP トランスポート、チェックサム タスク
- チェックサム タスク WDK ネットワーク
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: cb33ffb7a0ca2d022b4e2f20307656e092b6665e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368506"
---
# <a name="offloading-checksum-tasks"></a>チェックサム タスクのオフロード

NDIS は、実行時に TCP/IP チェックサム タスクをオフロードすることをサポートします。

> [!NOTE]
> チェックサム オフロード アウト オブ バンド (OOB) データが格納されている、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)情報の配列。 OOB のデータの詳細については、次を参照してください。 [TCP/IP Offload NET のへのアクセス\_バッファー\_情報を一覧表示](accessing-tcp-ip-offload-net-buffer-list-information.md)します。

NET ミニポート ドライバーに渡す前に\_バッファー\_リスト構造をパケットのミニポート ドライバーがチェックサム タスクを実行する場合は、TCP/IP トランスポートは NETに関連付けられているチェックサム情報を指定します\_バッファー\_リスト構造体。 この情報がで指定された、 [ **NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体は、ネットワークの一部である\_バッファー\_リストの情報 (帯域外のデータ)、NET に関連付けられている\_バッファー\_リスト構造体。

TCP パケットのチェックサムの計算をオフロードする前に、TCP/IP トランスポートは、1 の補数の合計 TCP pseudoheader を計算します。 TCP/IP トランスポートは、発信元 IP アドレス、宛先 IP アドレス、プロトコル、および TCP パケットの TCP の長さを含む、pseudoheader のすべてのフィールドの間で 1 の補数の合計を計算します。 TCP/IP トランスポートは、TCP ヘッダーのチェックサム フィールドに pseudoheader の 1 の補数の合計を入力します。

1 の補数の合計 TCP/IP トランスポートによって提供される pseudoheader は、送信パケットの実際の TCP チェックサムの計算にすぐに NIC を示します。 実際の TCP チェックサムを計算する NIC (TCP ヘッダーとペイロードで) の TCP チェックサムの可変部分を計算しますこのチェックサムに追加 1 の補数の合計、TCP/IP トランスポートによって計算 pseudoheader し、16 ビットの 1 つの計算の。チェックサムの補数。 このようなチェックサムを計算の詳細については、RFC 793 および RFC 1122 を参照してください。

> [!NOTE]
> TCP/IP トランスポートは、1 の補数の合計、pseudoheader TCP パケットの場合は、UDP ヘッダーのチェックサム フィールドに値を格納し、同じ手順を使用する UDP パケットを計算します。

TCP/IP トランスポートは、パケットの IP ヘッダーでチェックサム フィールドが、パケットを基になるミニポート ドライバーに渡す前に 0 に設定されているを常に保証されますに注意してください。 ミニポート ドライバーでは、IP ヘッダーでチェックサム フィールドを無視する必要があります。 ミニポート ドライバーは、チェックサム フィールドが 0 に設定されているし、このフィールドを 0 に設定する必要はありませんを確認する必要はありません。

NET を受け取った後\_バッファー\_リスト構造でその[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)または[ **MiniportCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数、ミニポート ドライバーは、次のチェックサム処理を通常は。

1.  ミニポート ドライバーの呼び出し、 [ **NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロが、  *\_Id* の**TcpIpChecksumNetBufferListInfo**を取得する、 [ **NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_リスト\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体。

2.  ミニポート ドライバーのテスト、 **IsIPv4**と**IsIPv6** NDIS フラグ\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報構造体。 どちらの場合、 **IsIPv4**と**IsIPv6**フラグが設定されていない、NIC は、パケットのチェックサム操作を実行する必要があります。

3.  場合、 **IsIPv4**または**IsIPv6**フラグが設定、ミニポート ドライバーのテスト、 **TcpChecksum**、 **UdpChecksum**、および**IpHeaderChecksum**チェックサム、パケットの NIC を計算する必要がありますを決定するフラグ。

4.  ミニポート ドライバーでは、パケットの適切なチェックサムを計算すると、NIC にパケットを渡します。 パケットにトンネル IP ヘッダーとトランスポート IP ヘッダーの両方がある場合は、IP チェックサム オフロードをサポートする NIC のみがトンネル ヘッダーの IP チェックサム タスクを実行します。 TCP/IP トランスポートは、トランスポートの IP ヘッダーの IP チェックサム タスクを実行します。

示す前に、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造チェックサムのタスクを実行する受信パケットの場合、ミニポート ドライバーが適切なチェックサムを検証します適切な設定と*Xxx * * * ChecksumFailed** または*Xxx * * * ChecksumSucceeded** フラグ、NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報構造体。

Large Send Offload (LSO) が有効な場合は、アドレス チェックサム オフロード オフにすると、コンピューティングと LSO 機能によって生成されたパケットにチェックサムを挿入するからミニポート ドライバーが防止されることはできません。 アドレス チェックサム オフロードを無効にするには、この場合、ユーザー必要がありますも無効に LSO。

 

 





