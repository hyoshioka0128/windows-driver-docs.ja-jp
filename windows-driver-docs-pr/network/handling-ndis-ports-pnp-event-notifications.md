---
title: NDIS ポートの PnP イベント通知
description: NDIS ポートの PnP イベント通知
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
ms.openlocfilehash: 331bc8ca32faad606225645ba75f447d90bf57b1
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565760"
---
# <a name="ndis-ports-pnp-event-notifications"></a>NDIS ポートの PnP イベント通知

ポートがアクティブ化または非アクティブ化されると、NDIS は PnP イベントを転送してドライバーに通知します。 ポートが割り当てられている場合、NDIS およびミニポートドライバーは PnP イベントを生成しません。 ミニポートドライバーは、ポートが**NetEventPortActivation** pnp イベントによってアクティブ化されたことを ndis に通知します。ミニポートドライバーは、一部のポートが非アクティブ化されたことを ndis に通知する**NetEventPortDeactivation** PnP イベントを生成します。

Ndis がプロトコルドライバーの[*protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、ndis は、現在アクティブなすべてのポート[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)の一覧を提供し*ます。BindParameters*パラメーター。

次のトピックでは、ポートの PnP イベントを処理する方法について説明します。

[ポートアクティブ化 PnP イベントの処理](handling-the-port-activation-pnp-event.md)

[ポートの非アクティブ化の PnP イベントの処理](handling-the-port-deactivation-pnp-event.md)

 

 





