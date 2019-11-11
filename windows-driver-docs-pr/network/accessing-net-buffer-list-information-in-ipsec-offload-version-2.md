---
title: IPsec オフロードバージョン2での NET_BUFFER_LIST 情報へのアクセス
description: IPsec Offload Version 2 での NET_BUFFER_LIST 情報へのアクセス
ms.assetid: 0c27b594-2c61-4459-96df-1d7445100bc5
keywords:
- IPsecOV2 WDK TCP/IP transport, NET_BUFFER_LIST 情報
- NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ff7547cbb48d2c0a72c74bd8d730032f9b95e83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838253"
---
# <a name="accessing-net_buffer_list-information-in-ipsec-offload-version-2"></a>IPsec オフロードバージョン2での NET\_BUFFER\_LIST 情報へのアクセス

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




NDIS では、net [ **\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**NetBufferListInfo**メンバーに帯域外 (OOB) データが提供されます。このデータは、 [**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造のリンクリストを指定します。 **NetBufferListInfo**メンバーは、リスト内のすべての NET\_バッファー構造に共通する情報を含む値の配列です。

次の識別子を[**NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロと共に使用して、IPsec オフロードバージョン 2 (IPsecOV2) の OOB データを**NetBufferListInfo**配列に設定して取得します。

<a href="" id="ipsecoffloadv2netbufferlistinfo"></a>**IPsecOffloadV2NetBufferListInfo**  
TCP/IP プロトコルから NIC への IPsec タスクのオフロードに使用される IPsecOV2 情報を指定します。 **IPsecOffloadV2NetBufferListInfo**、NET\_BUFFER\_list を指定すると\_情報は[**NDIS\_IPSEC\_オフロード\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)を返します。データ.

<a href="" id="ipsecoffloadv2tunnelnetbufferlistinfo"></a>**IPsecOffloadV2TunnelNetBufferListInfo**  
TCP/IP プロトコルから NIC への IPsec タスクのオフロードに使用される IPsecOV2 トンネル情報を指定します。 **IPsecOffloadV2TunnelNetBufferListInfo**、NET\_BUFFER\_list を指定すると\_情報は、 [**NDIS\_IPSEC\_オフロード\_V2\_トンネル\_NET\_BUFFER\_list @no_ を返し_t_13_ INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)構造体。\_

<a href="" id="ipsecoffloadv2headernetbufferlistinfo"></a>**IPsecOffloadV2HeaderNetBufferListInfo**  
[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)の IPsec ヘッダーのヘッダーオフセットと、次のヘッダーと埋め込み長の値を指定します。 **IPsecOffloadV2HeaderNetBufferListInfo**、NET\_BUFFER\_list を指定した場合\_情報は、 [**NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_BUFFER\_list を返し\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)構造体。

 

 





