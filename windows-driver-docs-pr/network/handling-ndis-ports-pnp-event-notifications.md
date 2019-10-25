---
title: NDIS ポート PnP イベント通知
description: NDIS ポート PnP イベント通知
ms.assetid: 2f542b62-43a0-42fa-b72d-f789e029d3f0
keywords:
- ポート WDK NDIS、PnP イベント通知
- NDIS ポート WDK、PnP イベント通知
- PnP イベント通知の WDK NDIS ポート
- イベント通知の WDK ネットワーク
- 通知 WDK ネットワーク
- 通知 WDK PnP、NDIS ポート
- イベント WDK networkin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d75ccf66dc32c5bd9912e996d3b55b194c372715
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842587"
---
# <a name="ndis-ports-pnp-event-notifications"></a>NDIS ポート PnP イベント通知

ポートがアクティブ化または非アクティブ化されると、NDIS は PnP イベントを転送してドライバーに通知します。 ポートが割り当てられている場合、NDIS およびミニポートドライバーは PnP イベントを生成しません。 ミニポートドライバーは、ポートが**NetEventPortActivation** pnp イベントによってアクティブ化されたことを ndis に通知します。ミニポートドライバーは、一部のポートが非アクティブ化されたことを ndis に通知する**NetEventPortDeactivation** PnP イベントを生成します。

NDIS がプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、ndis によって、 [**NDIS\_\_BIND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)の**activeports**メンバーで現在アクティブなすべてのポートの一覧が提供されます *。BindParameters*パラメーター。

次のトピックでは、ポートの PnP イベントを処理する方法について説明します。

[ポートアクティブ化 PnP イベントの処理](handling-the-port-activation-pnp-event.md)

[ポートの非アクティブ化の PnP イベントの処理](handling-the-port-deactivation-pnp-event.md)

 

 





