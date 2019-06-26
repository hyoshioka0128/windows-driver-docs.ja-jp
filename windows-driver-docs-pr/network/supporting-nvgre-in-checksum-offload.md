---
title: チェックサム オフロードでの NVGRE のサポート
description: このセクションでは、チェックサム オフロードで NVGRE のサポートについて説明します
ms.assetid: 933EE18B-917A-40BC-87AA-0F463615A082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a0e023142dcb03c9bd9f0e9968c29634680bc3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381182"
---
# <a name="supporting-nvgre-in-checksum-offload"></a>チェックサム オフロードでの NVGRE のサポート


NDIS 6.30 (Windows Server 2012) が導入されています[Network Virtualization using Generic Routing Encapsulation (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)します。 NDIS ミニポート、プロトコル、およびフィルター ドライバーおよび Nic チェックサム タスクの負荷を軽減する必要がありますで行う NVGRE をサポートする方法。

**注**  このページは、内の情報に精通していることを前提としています。[チェックサム タスクのオフロード](offloading-checksum-tasks.md)します。

 

場合[ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info).**IsEncapsulatedPacket**は**TRUE**と**TcpIpChecksumNetBufferListInfo**アウト オブ バンド (OOB) の情報が有効でこれを示すその NVGREサポートが必要ですし、NIC がトンネル (外部) の IP ヘッダー、トランスポート (内部) の IP ヘッダーと TCP または UDP ヘッダーのチェックサムを計算する必要があります。

**IsIPv4**と**IsIPv6**のフラグ、 [ **NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体は、トンネル (外部) の IP ヘッダーの IP ヘッダーのバージョンを指定します。 NIC には、そのヘッダーの IP バージョンを確認するトランスポート (内部) IP ヘッダーを解析する必要があります。 混合モードのパケットが許可されます (を参照してください[ **NDIS\_カプセル化\_パケット\_タスク\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload))、NIC を想定する必要がありますいない内部外部の IP ヘッダーで、同じ IP ヘッダー バージョンが必要があります。

Nic とミニポート ドライバーを使用して、可能性があります、 **InnerFrameOffset**、 **TransportIpHeaderRelativeOffset**、および**TcpHeaderRelativeOffset** で提供される値[ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)構造体。 NIC またはミニポート ドライバーでは、トンネル (外部) の IP ヘッダーまたはこれらのオフセットを検証する後続のヘッダーで、必要なヘッダーのチェックを実行できます。

場合[ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info).**IsEncapsulatedPacket**が true の場合、既存のヘッダー フィールドのオフセット[ **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info).**LsoV2Transmit**.**TcpHeaderOffset**と[ **NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info).**送信**.**TcpHeaderOffset**、適切な値はありませんし、NIC またはドライバーでは使用しないでください。

ミニポート ドライバーは、ケースを処理する必要があります、 [ **NDIS\_TCP\_送信\_オフロード\_補助的な\_NET\_バッファー\_ボックスの一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info).**InnerFrameOffset**パケットの先頭よりも、別のスキャッター/ギャザー リストがあります。 すべてのカプセル化の先頭に追加されたヘッダー (ETH、IP、GRE) が物理的に連続できるようになり、パケットの最初の MDL になります、プロトコルのドライバーが保証されます。

## <a name="checksum-validation"></a>チェックサムの検証


NVGRE のチェックサムの検証は、それ以外の場合にほぼ同じです。

ミニポートを受信した場合、 [OID\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) OID 要求が成功したのと**NDIS\_カプセル化\_型\_GRE\_MAC** (を参照してください[ **NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters))、NIC は、トンネル (でチェックサムの検証を実行する必要がありますIP ヘッダーの外側)、トランスポート (内部) の IP ヘッダーと TCP または UDP ヘッダー。

IPv4 トンネル (外側) ヘッダーと IPv4 トランスポート (内部) ヘッダーを持つパケットをカプセル化された、ミニポート ドライバーが設定する必要があります、 **IpChecksumSucceeded**フラグ、 [ **NDIS\_TCP\_IP\_チェックサム\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)両方 IP ヘッダーのチェックサム検証が成功した場合にのみを構造体します。 トンネル (外側) IPv4 ヘッダーとトランスポート (内部) IPv4 ヘッダーの両方を持つパケットをカプセル化された、ミニポート ドライバーが設定する必要があります、 **IpChecksumFailed** IP ヘッダーのチェックサムの検証のいずれかが失敗した場合にフラグを設定します。

 

 





