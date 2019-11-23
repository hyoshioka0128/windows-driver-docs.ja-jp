---
title: Large Send Offload (LSO) での NVGRE のサポート
description: このセクションでは、Large Send Offload (LSO) での NVGRE のサポートについて説明します。
ms.assetid: 1EB1B8C2-85C1-4256-BE96-C8B9F1D222B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c0cbb039154408e217fd85ad804fdea1bcf0c99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841794"
---
# <a name="supporting-nvgre-in-large-send-offload-lso"></a>Large Send Offload (LSO) での NVGRE のサポート


NDIS 6.30 (Windows Server 2012) では、[汎用ルーティングカプセル化 (NVGRE) を使用したネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)が導入されています。 大量の送信オフロード (LSO) バージョン 2 (LSOV2) を実行する NDIS ミニポート、プロトコル、およびフィルタードライバーと Nic は、NVGRE をサポートするようにする必要があります。

**注**  このページでは、[サイズの大きい TCP パケットのセグメント化のオフロード](offloading-the-segmentation-of-large-tcp-packets.md)に関する情報について理解していることを前提としています。

 

[**NDIS\_TCP\_送信\_\_補足\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)のオフロード。**IsEncapsulatedPacket**は**TRUE**で、 **TCPIPCHECKSUMNETBUFFERLISTINFO**の帯域外 (OOB) 情報が有効であることを示しています。これは、nvgre のサポートが必要であり、NIC が NVGRE 形式のパケットで LSOV2 オフロードを実行する必要があることを示しています。次のような状況があります。

-   [**NDIS\_TCP\_LARGE\_は、\_オフロード\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)の値のみを送信します。**LsoV2Transmit**構造体は有効です。 NIC とミニポートドライバーは、 **NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_BUFFER\_LIST\_INFO**の値を参照することはできません。**LsoV1Transmit**構造体。
-   [**NDIS\_TCP\_LARGE\_\_オフロード\_NET\_BUFFER\_LIST\_情報を送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)します。**LsoV2Transmit**。**Tcpheaderoffset**メンバーに正しいオフセット値が指定されていません。 NIC またはミニポートドライバーでは使用できません。

LSOV2 で NVGRE をサポートするには、プロトコルドライバーとフィルタードライバーで次の変更を行う必要があります。

-   [**NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)の**MSS**の値を小さくします。新しい GRE ヘッダーを考慮する**LsoV2Transmit**構造体。
-   短縮された**MSS**値の倍数ではない可能性のある TCP ペイロードの長さを送信します。
-   [**NDIS\_TCP\_送信\_オフロード\_補足\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)構造体を、GRE ヘッダーに対応するように**変更します**。

Nic およびミニポートドライバーでは、 [**NDIS\_TCP\_送信\_オフロード\_補足\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)構造体の**innerフレームオフセット**、 **TransportIpHeaderRelativeOffset**、および**TcpHeaderRelativeOffset**の値を使用できます。 NIC またはミニポートドライバーは、これらのオフセットを検証するために、トンネル (外部) IP ヘッダーまたはそれ以降のヘッダーに対して必要なヘッダーチェックを実行する場合があります。

ミニポートドライバーは、 [**NDIS\_TCP\_送信\_オフロード\_補足\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)の場合に対処する必要があります。**Innerフレームオフセット**は、パケットの先頭とは異なるスキャッター/ギャザーリストに存在する可能性があります。 プロトコルドライバーは、先頭にあるすべてのカプセル化ヘッダー (ETH、IP、GRE) が物理的に連続しており、パケットの最初の MDL に含まれることを保証します。

プロトコルおよびフィルタードライバーでは、TCP ペイロードの合計長が、減少した**MSS**値の正確な倍数であることは保証されません。 このため、ミニポートドライバーと Nic はトンネル (外部) IP ヘッダーを更新する必要があります。 Nic では、できるだけ多くの最大サイズのセグメントを生成する必要があります。これは、 [**NDIS\_TCP\_LARGE\_送信\_オフロード\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)**の値に**基づいて発生します。**LsoV2Transmit**OOB 情報。 LSOv2 send ごとに生成されるサブ**MSS**セグメントは1つだけです。

ミニポートドライバーは、次の操作を行う必要があります。

-   トンネル (外部) IP ヘッダーのチェックサムを計算します。
-   すべてのパケットについて、トンネル (外側) IP ヘッダーの IP 識別 (IP ID) 値を増やします。 最初のパケットでは、元のトンネル (外部) IP ヘッダーの IP ID を使用する必要があります。
-   すべてのパケットについて、トランスポート (内部) IP ヘッダーの IP ID を増やします。 最初のパケットでは、元のトランスポート (内部) IP ヘッダーの IP ID を使用する必要があります。
-   TCP ヘッダーとトランスポート (内部) IP ヘッダーのチェックサムを計算します。
-   生成されたすべてのパケットに、カプセル化トンネル (外側) ヘッダーを含む完全なヘッダーが追加されていることを確認します。

## <a name="related-topics"></a>関連トピック


[大きな TCP パケットのセグメント化のオフロード](offloading-the-segmentation-of-large-tcp-packets.md)

 

 






