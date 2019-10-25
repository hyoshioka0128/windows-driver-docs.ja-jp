---
title: NDIS ポートの管理
description: NDIS ポートの管理
ms.assetid: 08bb6623-aa9f-483e-a3cd-7dea676f3478
keywords:
- ポート WDK NDIS、管理
- NDIS ポート WDK、管理
- ポートの状態 WDK NDIS
- ポート番号 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0a83f97c068a33354bb05091cfd88bbcde129d2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844127"
---
# <a name="managing-an-ndis-port"></a>NDIS ポートの管理





関心のある NDIS ドライバーとユーザーモードアプリケーションでは、NDIS ポートを管理できます。 NDIS には、ポートを管理するためのサービスが用意されています。

NDIS は、関連付けられているステータスのインジケーターと PnP イベントを発行することにより、ポートの状態の変更を対象とする NDIS ドライバーおよびユーザーモードアプリケーションに通知します。

送信および受信機能に渡されるポート番号によって、送信操作または受信表示の発信元ポートが識別されます。 同様に、関連する構造体のポート番号によって、状態の表示、OID 要求、および PnP イベントのポートが識別されます。 ポート番号の詳細については、「 [NDIS Ports の概要](overview-of-ndis-ports.md)」を参照してください。

NDIS ポートを管理するために、次の構造にはポート番号が含まれています。

<a href="" id="ndis-oid-request"></a>[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
OID 要求について説明します。

<a href="" id="ndis-status-indication"></a>[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)  
NDIS の状態を示します。

<a href="" id="net-pnp-event-notification"></a>[**NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)  
PnP イベント通知について説明します。

このセクションの内容:

[NDIS ポートの送受信操作](ndis-port-send-and-receive-operations.md)

[NDIS ポート OID 要求](ndis-port-oid-requests.md)

[NDIS ポートの状態を処理する](handling-ndis-ports-status-indications.md)

[NDIS ポートの PnP イベント通知の処理](handling-ndis-ports-pnp-event-notifications.md)

 

 





