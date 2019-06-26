---
title: ポート アクティブ化 PnP イベントの処理
description: ポート アクティブ化 PnP イベントの処理
ms.assetid: 433018bf-daf5-4ea1-be3f-63349558f6b7
keywords:
- WDK NDIS、PnP イベント通知をポートします。
- NDIS ポート WDK、PnP イベント通知
- PnP イベント通知 WDK NDIS ポート
- PnP イベント WDK NDIS ポートのアクティブ化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 780918f40f98fb5a6523fbf2764848f7cb35de3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381332"
---
# <a name="handling-the-port-activation-pnp-event"></a>ポート アクティブ化 PnP イベントの処理





ドライバーの関連を処理する必要があります、 **NetEventPortActivation** PnP イベント ミニポート ドライバーには、NDIS ポートがアクティブにするとします。 NDIS では、既定のポートがアクティブ化されてまでプロトコル ドライバーとミニポート アダプター間のバインドは開始しません。 そのため、プロトコルのドライバーがへの呼び出しを扱う必要があります、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)既定のポートがアクティブである通知として機能します。

プロトコル ドライバーは、いない、ドライバーは、そのポートがアクティブで、バインド パラメーター、またはを通じて通知を受信した場合を除き、NDIS 要求のポート番号を使用する必要があります、 **NetEventPortActivation** PnP イベント。

NDIS イベントが生成されますポート アクティベーション PnP、ミニポート ドライバーにはいくつかのポートがアクティブにした後。 (ミニポート ドライバーを指定、 **NetEventPortActivation**イベントのコードでの PnP、 [ **NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)構造体、 *NetPnPEvent*への呼び出しでパラメーターが指す[ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent) NDIS ポートをアクティブにします)。

ミニポート ドライバーを使用して 1 つの PnP 通知で複数のポートのアクティブ化を示すことができます、**次**内のメンバー、 [ **NDIS\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port)をリンクする構造体複数の NDIS\_ポート構造体。 NDIS の詳細リンクのリストについて\_ポートの構造を参照してください[ライセンス NDIS ポート](activating-an-ndis-port.md)します。

NDIS 生成、 **NetEventPortDeactivation**ミニポートにいくつかのポートが非アクティブ化時にバインドされているプロトコル ドライバーに PnP イベント。 詳細については、 **NetEventPortDeactivation** PnP イベントは、「[ポート非アクティブ化の PnP イベントを処理する](handling-the-port-deactivation-pnp-event.md)します。

 

 





