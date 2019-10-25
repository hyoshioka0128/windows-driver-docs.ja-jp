---
title: フィルター モジュール PnP イベント通知
description: フィルター モジュール PnP イベント通知
ms.assetid: ca1e250a-aaa8-4fbc-abe5-c30c8913a67a
keywords:
- フィルターモジュール WDK ネットワーク、PnP イベント通知
- フィルタードライバー WDK ネットワーク、PnP イベント通知
- NDIS フィルタードライバー WDK、イベント通知
- イベント通知 WDK ネットワーク, フィルタードライバー
- WDK ネットワークプラグアンドプレイフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2f72de0277ff0334c8d2886067c82bdab0fe60e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838103"
---
# <a name="filter-module-pnp-event-notifications"></a>フィルター モジュール PnP イベント通知





フィルタードライバーは、基になるミニポートドライバーが受信するすべてのデバイスプラグアンドプレイ (PnP) 通知を受け取ることができます。 また、フィルタードライバーは、そのプロトコルドライバーが受信するすべてのネットワーク PnP 通知を受け取ることができます。PnP 通知の処理はドライバー固有です。

次の図は、フィルター処理されたデバイスの PnP イベント通知を示しています。

![フィルター処理されたデバイスのプラグアンドプレイイベント通知を示す図](images/pnpeventfilter.png)

フィルタードライバーは、デバイスの PnP と電源管理のイベント通知を渡すための NDIS 呼び出しを行う[*FilterDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_device_pnp_event_notify)関数を提供します。 これは、 [*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)関数に似ています。

フィルタードライバーは、デバイスの PnP と電源管理イベントを基になるドライバーに転送できます。 デバイスの PnP または電源管理イベントを転送するには、 [**NdisFDevicePnPEventNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdevicepnpeventnotify)関数を呼び出します。

次の図は、フィルター処理されたネットワーク PnP イベント通知を示しています。

![フィルター処理されたネットワークデバイスのプラグアンドプレイイベント通知を示す図](images/netpnpeventfilter.png)

フィルタードライバーは、NDIS 呼び出しによってネットワーク PnP および電源管理のイベント通知に渡す[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数を提供します。 これは、 [*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数に似ています。

フィルタードライバーは、ネットワークの PnP および電源管理イベントを今後のドライバーに転送できます。 ネットワーク PnP または電源管理イベントを転送するには、 [**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent)関数を呼び出します。

フィルタードライバーは、ドライバースタックの変更を処理する必要があります。 ドライバースタックの変更の詳細については、「[実行中のドライバースタックの変更](modifying-a-running-driver-stack.md)」を参照してください。

これらのイベントの処理を許可する必要がある場合、NDIS は PnP または電源管理の通知後に一時停止操作を開始できます。 詳細については、「[ドライバースタックの一時停止](pausing-a-driver-stack.md)」を参照してください。

 

 





