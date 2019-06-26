---
title: バインドの一時停止
description: バインドの一時停止
ms.assetid: 7f693904-d995-4fcb-8b88-9343a567602e
keywords:
- プロトコル ドライバー WDK ネットワークは、一時停止のバインド
- NDIS プロトコル ドライバー WDK、バインドの一時停止
- 一時停止 WDK ネットワークのバインド
- バインドは、WDK ネットワークを状態します。
- バインディング プロトコル ドライバーの一時停止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30bb08d8983f9bc3dc9a03c0f5ef27be204d684e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357594"
---
# <a name="pausing-a-binding"></a>バインドの一時停止





NDIS プロトコル ドライバーに送信した後、ネットワーク プラグ アンド プレイ (PnP) イベント通知は、バインドを一時停止、バインドは一時停止状態になります。

PnP の一時停止イベント、NDIS 呼び出しのプロトコル ドライバーに通知する、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)関数と、 **NetEvent**のメンバー、 [ **NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)構造に設定されている**NetEventPause**します。 **バッファー**メンバーが含まれています、 [ **NDIS\_プロトコル\_一時停止\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_pause_parameters)構造体。

プロトコル ドライバーの一時停止状態にバインドします。

-   新しい送信要求を開始する必要があります。

-   未処理の送信要求を完了を待つ必要があります。 NDIS 呼び出されるまでは一時停止操作が完了しない、 [ **ProtocolSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)未処理のドライバーのすべての関数は、要求を送信します。

-   ハンドルが表示されますがない通常どおりです。 基になるミニポート ドライバーが「未解決の待機を一時停止操作を完了する前に返すデータを受信します。 これにより、あることがなく継続的なミニポート ドライバーが一時停止した後に、ドライバー スタックで受信操作。

-   戻り値の新しい NDIS を示す直ちに受信します。 かどうか、必要に応じて、ドライバーをコピーできますなどに返す前にインジケーターを受信します。

プロトコル ドライバーの詳細については送信し受信操作を参照してください[プロトコル ドライバーの送信と受信操作](protocol-driver-send-and-receive-operations.md)します。

プロトコル ドライバーが完了した後、バインドが一時停止状態になる受信バインドの表示を返す未処理と NDIS は、すべてのバインディングの未処理の送信要求が完了します。

プロトコル ドライバーの一時停止状態にバインドします。

-   しないで要求を送信するいずれか。

-   戻り値がない直ちに受信します。 かどうか、必要に応じて、ドライバーをコピーできますなどに返す前にインジケーターを受信します。

 

 





