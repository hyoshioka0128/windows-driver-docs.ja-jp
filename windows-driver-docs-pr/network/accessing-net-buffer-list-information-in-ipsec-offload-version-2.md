---
title: IPsec オフロード バージョン 2 で NET_BUFFER_LIST 情報にアクセスします。
description: IPsec Offload Version 2 での NET_BUFFER_LIST 情報へのアクセス
ms.assetid: 0c27b594-2c61-4459-96df-1d7445100bc5
keywords:
- IPsecOV2 WDK TCP/IP トランスポート、NET_BUFFER_LIST 情報
- NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65f826f7ae3c64f2f951b49b98c95f5aa8f60c32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384427"
---
# <a name="accessing-netbufferlist-information-in-ipsec-offload-version-2"></a>NET にアクセスする\_バッファー\_IPsec オフロード バージョン 2 でリストの情報

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




NDIS でアウト オブ バンド (OOB) データを提供する、 **NetBufferListInfo**のメンバー、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体を指定します、リンク リスト[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。 **NetBufferListInfo**メンバーは、NET のすべてに共通する情報が含まれている値の配列\_リスト内のバッファーの構造体。

次の識別子を使用して、 [ **NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)設定および IPsec オフロード バージョン 2 (IPsecOV2) を取得するマクロ、でOOBデータ**NetBufferListInfo**配列。

<a href="" id="ipsecoffloadv2netbufferlistinfo"></a>**IPsecOffloadV2NetBufferListInfo**  
NIC に TCP/IP プロトコルからの IPsec タスク オフロードで使用される IPsecOV2 情報を指定します 指定すると**IPsecOffloadV2NetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)構造体。

<a href="" id="ipsecoffloadv2tunnelnetbufferlistinfo"></a>**IPsecOffloadV2TunnelNetBufferListInfo**  
NIC に TCP/IP プロトコルからの IPsec タスク オフロードで使用される IPsecOV2 トンネル情報を指定します 指定すると**IPsecOffloadV2TunnelNetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_IPSEC\_オフロード\_V2\_トンネル\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)構造体。

<a href="" id="ipsecoffloadv2headernetbufferlistinfo"></a>**IPsecOffloadV2HeaderNetBufferListInfo**  
IPsec ヘッダーでのヘッダー オフセットを指定します、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)と、次のヘッダーとパッドの長さの値。 指定すると**IPsecOffloadV2HeaderNetBufferListInfo**、NET\_バッファー\_一覧\_情報を返します、 [ **NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)構造体。

 

 





