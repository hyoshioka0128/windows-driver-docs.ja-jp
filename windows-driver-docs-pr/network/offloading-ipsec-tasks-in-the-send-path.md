---
title: 送信パスでの IPsec タスクのオフロード
description: 送信パスでの IPsec タスクのオフロード
ms.assetid: b95878e0-0aee-43cb-a64c-b5d8e07cb1b4
keywords:
- WDK IPsec オフロード、ESP により保護されたパケットの送信パスのオフロード
- WDK IPsec オフロード、AH で保護されたパケットの送信パスのオフロード
- パスのオフロード WDK IPsec オフロードを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cca612ce12aaae1a3628e2679cdb41d83abe039
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368495"
---
# <a name="offloading-ipsec-tasks-in-the-send-path"></a>送信パスでの IPsec タスクのオフロード

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




TCP/IP トランスポートは、ミニポート ドライバーに渡される前に、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) NIC がインターネット プロトコル セキュリティ (IPsec) を実行するパケットの構造ネットワークに関連付けられている IPsec 情報更新タスク、\_バッファー\_リスト構造体。 TCP/IP トランスポートでは、この情報を指定します、 [ **NDIS\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)構造体は、ネットワークの一部である\_バッファー\_リストの情報 (帯域外のデータ)、NET に関連付けられている\_バッファー\_リスト構造体。

TCP/IP トランスポートを提供*OffloadHandle*トランスポート (エンド ツー エンド接続) 部分の送信パケットの送信、SA を識別するハンドルを指定します。 パケットは、トンネル経由送信は、指定すると、TCP/IP トランスポートも提供*NextOffloadHandle*、送信パケットの部分のトンネルの送信、SA を識別するハンドルを指定します。

ドライバーの受信後、ミニポート、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体の[ *MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)または[ **MiniportCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数を呼び出すことが、 [ **NET\_バッファー\_ボックスの一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)マクロが、  *\_Id*の**IPsecOffloadV1NetBufferListInfo** NDIS を取得する\_IPSEC\_オフロード\_V1\_NET\_バッファー\_一覧\_NET に関連付けられている情報の構造体\_バッファー\_リスト構造体。

NIC は、IPsec の送信パケットの処理を実行するときに、パケットの (またはその両方) を AH または ESP 暗号化チェックサムを計算し、パケットには、ESP ペイロードが含まれている場合は、パケットを暗号化します。 TCP/IP トランスポートが既にパケットをフレーム化、し (必要に応じて) が埋め込まれておよびシーケンス番号および SPI 割り当てられています。

 

 





