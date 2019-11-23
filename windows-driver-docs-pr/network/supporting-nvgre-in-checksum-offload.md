---
title: チェックサム オフロードでの NVGRE のサポート
description: このセクションでは、チェックサムオフロードでの NVGRE のサポートについて説明します。
ms.assetid: 933EE18B-917A-40BC-87AA-0F463615A082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9b698da69fcc65bf31aea0c91bb79f9b330d869
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841796"
---
# <a name="supporting-nvgre-in-checksum-offload"></a>チェックサム オフロードでの NVGRE のサポート


NDIS 6.30 (Windows Server 2012) では、[汎用ルーティングカプセル化 (NVGRE) を使用したネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)が導入されています。 チェックサムタスクをオフロードする NDIS ミニポート、プロトコル、フィルタードライバーと Nic は、NVGRE をサポートするようにする必要があります。

この**ページ  、** [チェックサムタスクのオフロード](offloading-checksum-tasks.md)に関する情報を把握していることを前提としています。

 

[**NDIS\_TCP\_送信\_\_補足\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)のオフロード。**IsEncapsulatedPacket**は**TRUE**で、 **TCPIPCHECKSUMNETBUFFERLISTINFO**の帯域外 (OOB) 情報が有効であることを示します。これは、nvgre のサポートが必要であり、NIC がトンネル (外部) ip ヘッダー、トランスポート (内部) ip ヘッダー、および TCP または UDP ヘッダーのチェックサムを計算する必要があることを示します。

[**NDIS\_TCP\_IP\_チェックサム\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体の**IsIPv4**および**IsIPv6**フラグは、トンネル (外部) ip ヘッダーの ip ヘッダーバージョンを示します。 NIC は、トランスポート (内部) IP ヘッダーを解析して、そのヘッダーの IP バージョンを判断する必要があります。 混合モードパケットは許可されているため (「 [**NDIS\_カプセル化\_パケット\_タスク\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload))」を参照してください。そのため、NIC では、内部と外部の ip ヘッダーが同じ ip ヘッダーバージョンであると想定することはできません。

Nic およびミニポートドライバーでは、 [**NDIS\_TCP\_送信\_オフロード\_補足\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)構造体の**innerフレームオフセット**、 **TransportIpHeaderRelativeOffset**、および**TcpHeaderRelativeOffset**の値を使用できます。 NIC またはミニポートドライバーは、これらのオフセットを検証するために、トンネル (外部) IP ヘッダーまたはそれ以降のヘッダーに対して必要なヘッダーチェックを実行する場合があります。

[**NDIS\_TCP\_送信\_、\_補足\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)にオフロードすることに注意してください。**IsEncapsulatedPacket**が TRUE の場合、既存のヘッダーオフセットフィールドである[**NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)ます。**LsoV2Transmit**。**Tcpheaderoffset**および[**NDIS\_TCP\_IP\_チェックサム\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)。**送信**。**Tcpheaderoffset**は正しい値を持たず、NIC またはドライバーでは使用できません。

ミニポートドライバーは、 [**NDIS\_TCP\_送信\_オフロード\_補足\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)の場合に対処する必要があります。**Innerフレームオフセット**は、パケットの先頭とは異なるスキャッター/ギャザーリストに存在する可能性があります。 プロトコルドライバーは、先頭にあるすべてのカプセル化ヘッダー (ETH、IP、GRE) が物理的に連続しており、パケットの最初の MDL に含まれることを保証します。

## <a name="checksum-validation"></a>チェックサムの検証


NVGRE のチェックサムの検証は、それ以外の場合とほぼ同じです。

ミニポートが Oid を受信し[\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)の oid 要求を受け取り、それを**NDIS\_カプセル化**( [**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)を参照) に対して成功させる場合、NIC はトンネル (外部) ip ヘッダー、トランスポート (内部) IP ヘッダー、TCP または UDP ヘッダーに対してチェックサム検証を実行する必要があります。\_\_\_

IPv4 トンネル (外側) ヘッダーと IPv4 トランスポート (内部) ヘッダーを持つカプセル化されたパケットの場合、 **IpChecksumSucceeded**フラグは、ip ヘッダーのチェックサム検証が正常に完了した場合にのみ、 [**NDIS\_TCP\_IP\_チェックサム\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)構造体に設定する必要があります。 トンネル (外部) IPv4 ヘッダーとトランスポート (内部) IPv4 ヘッダーの両方を持つカプセル化されたパケットの場合、いずれかの IP ヘッダーチェックサム検証が失敗した場合、ミニポートドライバーは**IpChecksumFailed**フラグを設定する必要があります。

 

 





