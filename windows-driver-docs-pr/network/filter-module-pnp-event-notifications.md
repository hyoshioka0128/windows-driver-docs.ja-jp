---
title: フィルター モジュール PnP イベント通知
description: フィルター モジュール PnP イベント通知
ms.assetid: ca1e250a-aaa8-4fbc-abe5-c30c8913a67a
keywords:
- モジュールの WDK ネットワークをフィルター処理、イベント通知の PnP
- イベント通知の PnP ドライバー WDK ネットワークをフィルターで、
- NDIS フィルター ドライバー WDK、イベント通知
- イベント通知の WDK ネットワー キング、フィルター ドライバー
- プラグ アンド プレイ WDK ネットワー キング、フィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dacf5af6377f848e11cd584f43582fc83f2b33ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363416"
---
# <a name="filter-module-pnp-event-notifications"></a>フィルター モジュール PnP イベント通知





フィルター ドライバーは、(すべて、デバイス プラグ アンド プレイ PnP) 通知を基になるミニポート ドライバーの受信を受信できます。 また、フィルター ドライバーは、上位のプロトコルのドライバーが表示されるすべてのネットワーク PnP 通知を受信することができます。PnP 通知の処理は、特定のドライバーです。

次の図は、フィルター選択されたデバイスの PnP イベント通知を示しています。

![フィルター選択されたデバイスのプラグ アンド プレイのイベント通知を示す図](images/pnpeventfilter.png)

フィルター ドライバーを提供する[ *FilterDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_device_pnp_event_notify) NDIS を渡すデバイス PnP、電源管理のイベント通知で呼び出される関数。 これに似ています、 [ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)関数。

フィルター ドライバーは、基になるドライバーにデバイス PnP、電源管理イベントを転送できます。 デバイスの電源または PnP 管理イベントを転送するには、呼び出し、 [ **NdisFDevicePnPEventNotify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfdevicepnpeventnotify)関数。

次の図は、フィルター選択されたネットワーク PnP イベント通知を示しています。

![フィルター選択されたネットワーク デバイスのプラグ アンド プレイのイベント通知を示す図](images/netpnpeventfilter.png)

フィルター ドライバーを提供する[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)ネットワーク PnP、電源管理のイベント通知に渡す NDIS が呼び出す関数です。 これに似ています、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)関数。

フィルター ドライバーがドライバーに関連するネットワーク PnP、電源管理イベントを転送できます。 ネットワークの PnP または電源管理イベントを転送するには、呼び出し、 [ **NdisFNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfnetpnpevent)関数。

フィルター ドライバーはドライバー スタックの変更を処理する必要があります。 ドライバー スタックの変更の詳細については、次を参照してください。[変更を実行しているドライバー スタック](modifying-a-running-driver-stack.md)します。

これらのイベントの処理を許可する必要がある場合、NDIS は PnP 後の一時停止操作または電源管理の通知を開始できます。 詳細については、次を参照してください。[ドライバー スタックを一時停止](pausing-a-driver-stack.md)します。

 

 





