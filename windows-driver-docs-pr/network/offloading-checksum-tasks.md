---
title: チェックサム タスクのオフロード
description: チェックサム タスクのオフロード
ms.assetid: 5fb2f379-c357-4ec3-b103-bdbe23fcc033
keywords:
- タスクオフロード WDK TCP/IP トランスポート、チェックサムタスク
- チェックサムタスク (WDK ネットワーク)
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: b8f5f83914519db0a820c1d234018b20f930df1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844329"
---
# <a name="offloading-checksum-tasks"></a>チェックサム タスクのオフロード

NDIS は、実行時の TCP/IP チェックサムタスクのオフロードをサポートしています。

> [!NOTE]
> チェックサムオフロード帯域外 (OOB) データは、 [**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)情報配列に格納されます。 OOB データの詳細については、「 [Tcp/ip オフロード NET\_BUFFER\_LIST 情報へのアクセス](accessing-tcp-ip-offload-net-buffer-list-information.md)」を参照してください。

ミニポートドライバーに渡す前に、ミニポートドライバーがチェックサムタスクを実行するパケットの NET\_BUFFER\_LIST 構造体を、TCP/IP トランスポートは、NET\_バッファーに関連付けられているチェックサム情報を指定し @no__ 形式のリスト構造。 この情報は、 [**NDIS\_TCP\_IP\_CHECKSUM\_net\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体によって指定されます。これは、NET\_BUFFER\_list 情報の一部です (帯域外データ)。これは、NET\_BUFFER\_LIST 構造体に関連付けられています。

Tcp パケットのチェックサム計算をオフロードする前に、tcp/ip トランスポートは TCP 擬似ヘッダーの1の補数の合計を計算します。 TCP/IP トランスポートは、擬似ヘッダー内のすべてのフィールドの1の補数の合計を計算します。これには、送信元 IP アドレス、宛先 IP アドレス、プロトコル、TCP パケットの TCP の長さが含まれます。 Tcp/ip トランスポートは、TCP ヘッダーの Checksum フィールドに、擬似ヘッダーの1の補数合計を入力します。

TCP/IP トランスポートによって提供される疑似ヘッダーの補数合計により、NIC は、送信パケットの実際の TCP チェックサムの計算を初期段階で開始します。 実際の TCP チェックサムを計算するために、NIC は tcp チェックサムの可変部分 (TCP ヘッダーおよびペイロード用) を計算し、このチェックサムを TCP/IP トランスポートによって計算された擬似ヘッダーの1の補数の合計に追加し、16ビットの1を計算します。チェックサムを補完します。 このようなチェックサムの計算の詳細については、RFC 793 および RFC 1122 を参照してください。

> [!NOTE]
> TCP/IP トランスポートは、TCP パケットの場合と同じ手順を使用して UDP パケットの疑似ヘッダーの1の補数の合計を計算し、UDP ヘッダーの Checksum フィールドに値を格納します。

TCP/IP トランスポートでは、パケットが基になるミニポートドライバーに渡される前に、パケットの IP ヘッダーのチェックサムフィールドが常に0に設定されていることに注意してください。 ミニポートドライバーは、IP ヘッダーのチェックサムフィールドを無視する必要があります。 ミニポートドライバーでは、チェックサムフィールドがゼロに設定されていることを確認する必要はありません。このフィールドを0に設定する必要はありません。

ミニポート[*sendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数または[**Miniportcosendnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数で NET\_BUFFER\_LIST 構造を受け取ると、通常、ミニポートドライバーは次のチェックサム処理を実行します。

1.  ミニポートドライバーは、 *\_Id*が**TcpIpChecksumNetBufferListInfo**の[**net\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロを呼び出して、 [**NDIS\_TCP\_IP\_CHECKSUM\_net を取得します。\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体です。

2.  ミニポートドライバーは、NDIS\_TCP\_IP\_チェックサム\_NET\_BUFFER\_LIST\_INFO 構造体の**IsIPv4**および**IsIPv6**フラグをテストします。 **IsIPv4**と**IsIPv6**の両方のフラグが設定されていない場合、NIC はパケットに対してチェックサム操作を実行しません。

3.  **IsIPv4**または**IsIPv6**フラグが設定されている場合、ミニポートドライバーは**tcpchecksum**、 **UdpChecksum**、および**IPHEADERCHECKSUM**の各フラグをテストして、NIC がパケットに対して計算する必要があるチェックサムを判別します。

4.  ミニポートドライバーは、パケットを NIC に渡します。これにより、パケットの適切なチェックサムが計算されます。 パケットにトンネル IP ヘッダーとトランスポート IP ヘッダーの両方がある場合、IP チェックサムのオフロードをサポートする NIC は、トンネルヘッダーでのみ IP チェックサムタスクを実行します。 TCP/IP トランスポートは、トランスポート IP ヘッダーで IP チェックサムタスクを実行します。

チェックサムタスクを実行する受信パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を示す前に、ミニポートドライバーは適切なチェックサムを検証し、適切な*Xxx ** * * ChecksumFailed * または*xxx * * を設定します。* ChecksumSucceeded** NDIS\_TCP\_IP\_チェックサム\_NET\_BUFFER\_LIST\_INFO 構造体のフラグ。

サイズの大きい送信オフロード (LSO) が有効になっている場合に、アドレスチェックサムのオフロードをオフにしても、ミニポートドライバーは、LSO 機能によって生成されたパケットにチェックサムを計算して挿入することはできません。 この場合、アドレスチェックサムのオフロードを無効にするには、ユーザーは LSO も無効にする必要があります。

 

 





