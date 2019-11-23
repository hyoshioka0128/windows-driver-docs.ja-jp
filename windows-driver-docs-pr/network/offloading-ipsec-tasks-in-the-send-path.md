---
title: 送信パスでの IPsec タスクのオフロード
description: 送信パスでの IPsec タスクのオフロード
ms.assetid: b95878e0-0aee-43cb-a64c-b5d8e07cb1b4
keywords:
- ESP で保護されたパケットの WDK IPsec オフロード、送信パスオフロード
- AH で保護されたパケット WDK IPsec オフロード、送信パスオフロード
- 送信パスオフロード WDK IPsec オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 762ff85b05589f46367f6fa4e1ed20a8c1934cdb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834613"
---
# <a name="offloading-ipsec-tasks-in-the-send-path"></a>送信パスでの IPsec タスクのオフロード

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




TCP/IP トランスポートがミニポートドライバーに渡す前に、NIC がインターネットプロトコルセキュリティ (IPsec) タスクを実行するパケットの[**net\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を使用して、NET\_BUFFER\_LIST 構造に関連付けられている IPsec 情報を更新します。 TCP/IP トランスポートでは、 [**NDIS\_IPSEC\_オフロード\_V1\_net\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)構造体の情報を指定します。これは、net\_buffer\_list 構造に関連付けられている NET\_BUFFER\_list 情報 (帯域外データ) の一部です。

TCP/IP トランスポートは*Offloadhandle*を提供します。これは、送信パケットのトランスポート (エンドツーエンド接続) 部分の送信 SA へのハンドルを指定します。 パケットがトンネルを介して送信される場合、TCP/IP トランスポートは、送信パケットのトンネル部分の送信 SA へのハンドルを指定する*Nextoffloadhandle*も提供します。

ミニポートドライバーは、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数または[**Miniportcosendnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数で[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を受け取ると、 **IPsecOffloadV1NetBufferListInfo**の *\_ID*を使用して[**net\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロを呼び出して、NDIS\_IPSEC\_オフロード\_V1\_NET\_BUFFER\_LIST\_info 構造を取得できます。NET\_BUFFER\_LIST 構造体に関連付けられています。

NIC は、送信パケットで IPsec 処理を実行するときに、パケットに対して AH または ESP の暗号化チェックサム (またはその両方) を計算し、パケットに ESP ペイロードが含まれている場合はパケットを暗号化します。 TCP/IP トランスポートでは、既にパケットのフレームが付けられ、必要に応じて埋め込まれ、シーケンス番号と SPI に割り当てられています。

 

 





