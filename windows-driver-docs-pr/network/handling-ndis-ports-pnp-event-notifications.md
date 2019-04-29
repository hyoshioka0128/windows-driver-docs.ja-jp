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
ms.openlocfilehash: 07bcf268e4921825d623e4c9454b77de5086be06
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330872"
---
# <a name="handling-ndis-ports-pnp-event-notifications"></a>NDIS ポート PnP イベント通知の処理





NDIS は、ポートがアクティブ化または非アクティブ化されたときに、上にあるドライバーを通知する PnP イベントを転送します。 NDIS ミニポート ドライバーでは、ポートが割り当てられるときに、PnP イベントは生成されません。 ミニポート ドライバーに通知をアクティブになったポート NDIS、 **NetEventPortActivation** PnP イベントおよびミニポート ドライバーの生成、 **NetEventPortDeactivation** PnP 通知するイベントを NDIS の一部ポートが無効になりました。

NDIS を呼び出すと、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)プロトコル ドライバー、NDIS の関数で現在アクティブなすべてのポートの一覧を提供する、 **ActivePorts** のメンバー[**NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)で構造体、 *BindParameters*パラメーター。

次のトピックでは、ポート PnP イベントを処理する方法について説明します。

[ポート アクティベーション PnP イベントを処理します。](handling-the-port-activation-pnp-event.md)

[ポートの非アクティブ化の PnP イベントを処理します。](handling-the-port-deactivation-pnp-event.md)

 

 





