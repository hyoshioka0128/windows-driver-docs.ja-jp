---
title: プロトコル ドライバーの PnP イベント通知の処理
description: プロトコル ドライバーの PnP イベント通知の処理
ms.assetid: 7c6c9bc5-37ce-49f4-8e39-5f51a266836a
keywords:
- プラグアンドプレイ WDK NDIS プロトコル
- 通知 WDK PnP, NDIS プロトコルドライバー
- イベント通知の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d11b7a42493cd60c13a0f3c0e7477634161fbab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842571"
---
# <a name="handling-pnp-event-notifications-in-a-protocol-driver"></a>プロトコル ドライバーの PnP イベント通知の処理





NDIS 6.0 以降のプロトコルドライバーは、NDIS 6.0 以降に固有のイベント通知に加えて、NDIS 5.x ドライバーと同じプラグアンドプレイ (PnP) イベント通知を処理します。 PnP イベント通知の処理は、ドライバー固有です。

プロトコルドライバーにネットワークの PnP イベントを通知するために、NDIS はドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 イベントの種類とイベントの特性を定義するために、NDIS は*ProtocolNetPnPEvent*の*NetPnPEvent*イベントパラメーターに[**NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)構造体を渡します。

プロトコルドライバーは、ドライバースタックの変更を処理する必要があります。 ドライバースタックの変更の詳細については、「[実行中のドライバースタックの変更](modifying-a-running-driver-stack.md)」を参照してください。

スタック変更通知を処理しないプロトコルドライバーは、アダプターからバインド解除され、再バインドされます。 ドライバースタック通知を正常に処理するプロトコルドライバーのバインドには影響しません。

プロトコルドライバーは、ドライバースタックの一時停止通知を処理する必要があります。 これらの通知の詳細については、「[ドライバースタックの一時停止](pausing-a-driver-stack.md)」を参照してください。

プロトコルドライバーは、ドライバースタックの再起動通知を処理する必要があります。 これらの通知の詳細については、「[ドライバースタックの再起動](restarting-a-driver-stack.md)」を参照してください。

 

 





