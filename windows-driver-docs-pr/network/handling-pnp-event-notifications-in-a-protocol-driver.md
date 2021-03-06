---
title: プロトコル ドライバーの PnP イベント通知の処理
description: プロトコル ドライバーの PnP イベント通知の処理
ms.assetid: 7c6c9bc5-37ce-49f4-8e39-5f51a266836a
keywords:
- プラグ アンド プレイ WDK NDIS プロトコル
- WDK PnP、NDIS プロトコル ドライバーに通知
- イベント通知の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a68625b8caae2096233e9b5ff811568afba7a2f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379780"
---
# <a name="handling-pnp-event-notifications-in-a-protocol-driver"></a>プロトコル ドライバーの PnP イベント通知の処理





NDIS 6.0 とそれ以降のプロトコル ドライバーは、NDIS 6.0 以降、固有のイベント通知のほか、NDIS 5.x ドライバーとして同じのプラグ アンド プレイ (PnP) イベント通知を処理します。 PnP イベント通知の処理は、特定のドライバーです。

NDIS ドライバーの呼び出しのネットワークの PnP イベント プロトコル ドライバーに通知する[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)関数。 NDIS を通過するイベントのイベントの種類と特性を定義する、 [ **NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)で構造体、 *NetPnPEvent*イベント パラメーターの*ProtocolNetPnPEvent*します。

プロトコル ドライバーには、ドライバー スタックの変更を処理する必要があります。 ドライバー スタックの変更の詳細については、次を参照してください。[変更を実行しているドライバー スタック](modifying-a-running-driver-stack.md)します。

スタックの変更通知を処理しないプロトコル ドライバーは、アダプターと再バインドからバインドではありません。 ドライバー スタックの通知を正常に処理するプロトコル ドライバーのバインドには影響しません。

プロトコル ドライバーには、ドライバー スタックの一時停止の通知を処理する必要があります。 これらの通知の詳細については、次を参照してください。[ドライバー スタックを一時停止](pausing-a-driver-stack.md)します。

プロトコル ドライバーには、ドライバー スタックの再起動の通知を処理する必要があります。 これらの通知の詳細については、次を参照してください。[ドライバー スタックの再起動](restarting-a-driver-stack.md)します。

 

 





