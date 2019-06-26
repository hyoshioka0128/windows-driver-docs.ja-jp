---
title: CoNDIS コール マネージャーまたは MCM を閉じる
description: CoNDIS コール マネージャーまたは MCM を閉じる
ms.assetid: 6ef64e4c-eec4-4477-a06c-f80e21d5b1c7
keywords:
- コール マネージャーの WDK ネットワー キング、いる CoNDIS
- MCMs WDK ネットワー キング、閉じる
- 閉じる、ミニポート コール マネージャー WDK ネットワーク
- 終了呼び出しマネージャー
- ミニポート コール マネージャーを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0682b19b8f16426a27b267bcb2b049fd78b81101
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384222"
---
# <a name="closing-a-condis-call-manager-or-mcm"></a>CoNDIS コール マネージャーまたは MCM を閉じる





ときに、スタンドアロンのコール マネージャーは、基になるミニポート アダプターからバインド解除、コール マネージャーする必要がありますに通知のすべての影響を受けるいる CoNDIS クライアント関連 AF を閉じる必要があります。 各クライアントを通知するスタンドアロンの NDIS 呼び出しマネージャー、 [ **NdisCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)関数。

MCM を管理している CoNDIS ミニポート アダプターが停止する場合、MCM する必要がありますに通知のすべての影響を受けるクライアント関連 AF を閉じる必要があります。 MCMs 呼び出しは、各クライアントに通知する、 [ **NdisMCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)関数。

スタンドアロンのコール マネージャーまたは MCM を呼び出す場合**NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**、それぞれ、NDIS 呼び出し、 [ **ProtocolClNotifyCloseAf** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_notify_close_af)のハンドルに関連付けられているいる CoNDIS クライアントの機能、 *NdisAfHandle*パラメーターの**NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**します。 この呼び出しは、クライアントを閉じる、AF を通知します。 場合**NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**返します NDIS\_状態\_保留中、NDIS は呼び出しをマネージャーの[**ProtocolCmNotifyCloseAfComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_notify_close_af_complete)通知の閉じる操作の完了時に機能します。

閉じている CoNDIS クライアントで、アドレス ファミリの詳細については、次を参照してください。[いる CoNDIS クライアントで、アドレス ファミリを閉じる](closing-an-address-family-in-a-condis-client.md)します。

 

 





