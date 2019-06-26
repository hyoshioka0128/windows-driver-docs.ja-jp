---
title: NDIS ポート PnP イベント通知の処理
description: NDIS ポート PnP イベント通知の処理
ms.assetid: 2f542b62-43a0-42fa-b72d-f789e029d3f0
keywords:
- WDK NDIS、PnP イベント通知をポートします。
- NDIS ポート WDK、PnP イベント通知
- PnP イベント通知 WDK NDIS ポート
- イベント通知の WDK ネットワーク
- 通知の WDK ネットワーク
- 通知 WDK PnP、NDIS ポート
- イベントの WDK ネットワーク経由
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69aca41a9c7c18db1400ffb840ca167a594b202a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379819"
---
# <a name="handling-ndis-ports-pnp-event-notifications"></a>NDIS ポート PnP イベント通知の処理





NDIS は、ポートがアクティブ化または非アクティブ化されたときに、上にあるドライバーを通知する PnP イベントを転送します。 NDIS ミニポート ドライバーでは、ポートが割り当てられるときに、PnP イベントは生成されません。 ミニポート ドライバーに通知をアクティブになったポート NDIS、 **NetEventPortActivation** PnP イベントおよびミニポート ドライバーの生成、 **NetEventPortDeactivation** PnP 通知するイベントを NDIS の一部ポートが無効になりました。

NDIS を呼び出すと、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)プロトコル ドライバー、NDIS の関数で現在アクティブなすべてのポートの一覧を提供する、 **ActivePorts** のメンバー[**NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)で構造体、 *BindParameters*パラメーター。

次のトピックでは、ポート PnP イベントを処理する方法について説明します。

[ポート アクティベーション PnP イベントを処理します。](handling-the-port-activation-pnp-event.md)

[ポートの非アクティブ化の PnP イベントを処理します。](handling-the-port-deactivation-pnp-event.md)

 

 





