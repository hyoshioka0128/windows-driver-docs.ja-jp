---
title: バインドの一時停止
description: バインドの一時停止
ms.assetid: 7f693904-d995-4fcb-8b88-9343a567602e
keywords:
- プロトコルドライバー WDK ネットワーク、バインドの一時停止
- NDIS プロトコルドライバー WDK、バインドの一時停止
- バインド一時停止 WDK ネットワーク
- バインドの状態 WDK ネットワーク
- プロトコルドライバーのバインドを一時停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6e53cff2b9f7522dd4ade77ceca5c08e7cbf865
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843701"
---
# <a name="pausing-a-binding"></a>バインドの一時停止





NDIS がプロトコルドライバーを送信すると、ネットワークプラグアンドプレイ (PnP) によってバインドのイベント通知が一時停止されます。このバインディングは、一時停止中の状態になります。

プロトコルドライバーに PnP pause イベントを通知するために、NDIS は[**NET\_PnP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)の**netevent**メンバーを使用して[*PROTOCOLNETPNPEVENT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出し\_通知構造体は**NetEventPause**に設定されています。 **バッファー**メンバーには、 [ **\_PARAMETERS 構造\_一時停止する NDIS\_プロトコル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_pause_parameters)が含まれています。

一時停止中の状態のバインディングの場合、プロトコルドライバーは次のようになります。

-   新しい送信要求を開始することはできません。

-   未処理の送信要求が完了するまで待機する必要があります。 この一時停止操作は、NDIS がすべてのドライバーの未処理の送信要求に対して[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)関数を呼び出すまで完了しません。

-   受信の表示は通常どおりに処理する必要があります。 基になるミニポートドライバーは、一時停止操作が完了する前に、未処理の受信データが返されるのを待機します。 これにより、ミニポートドライバーが一時停止した後に、ドライバースタックに実行中の受信操作がないことが保証されます。

-   新しい受信の表示を NDIS に直ちに返す必要があります。 必要に応じて、ドライバーはこのような受信表示をコピーしてから返すようにすることができます。

プロトコルドライバーの送受信操作の詳細については、「[プロトコルドライバーの送信および受信操作](protocol-driver-send-and-receive-operations.md)」を参照してください。

バインドに対する未処理の受信通知を返すプロトコルドライバーが完了すると、バインディングは一時停止状態になり、NDIS はバインドに対する未処理の送信要求をすべて完了します。

一時停止状態のバインドの場合、プロトコルドライバーは次のようになります。

-   送信要求を作成することはできません。

-   は、すぐに受信表示を返します。 必要に応じて、ドライバーはこのような受信表示をコピーしてから返すようにすることができます。

 

 





