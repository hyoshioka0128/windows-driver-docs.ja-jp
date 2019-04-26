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
ms.openlocfilehash: f96ec7e9531a65b5d3720c04e53609a9429c495e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350043"
---
# <a name="filter-module-pnp-event-notifications"></a>フィルター モジュール PnP イベント通知





フィルター ドライバーは、(すべて、デバイス プラグ アンド プレイ PnP) 通知を基になるミニポート ドライバーの受信を受信できます。 また、フィルター ドライバーは、上位のプロトコルのドライバーが表示されるすべてのネットワーク PnP 通知を受信することができます。PnP 通知の処理は、特定のドライバーです。

次の図は、フィルター選択されたデバイスの PnP イベント通知を示しています。

![フィルター選択されたデバイスのプラグ アンド プレイのイベント通知を示す図](images/pnpeventfilter.png)

フィルター ドライバーを提供する[ *FilterDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff549926) NDIS を渡すデバイス PnP、電源管理のイベント通知で呼び出される関数。 これに似ています、 [ *MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)関数。

フィルター ドライバーは、基になるドライバーにデバイス PnP、電源管理イベントを転送できます。 デバイスの電源または PnP 管理イベントを転送するには、呼び出し、 [ **NdisFDevicePnPEventNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff561804)関数。

次の図は、フィルター選択されたネットワーク PnP イベント通知を示しています。

![フィルター選択されたネットワーク デバイスのプラグ アンド プレイのイベント通知を示す図](images/netpnpeventfilter.png)

フィルター ドライバーを提供する[ *FilterNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff549952)ネットワーク PnP、電源管理のイベント通知に渡す NDIS が呼び出す関数です。 これに似ています、 [ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)関数。

フィルター ドライバーがドライバーに関連するネットワーク PnP、電源管理イベントを転送できます。 ネットワークの PnP または電源管理イベントを転送するには、呼び出し、 [ **NdisFNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561828)関数。

フィルター ドライバーはドライバー スタックの変更を処理する必要があります。 ドライバー スタックの変更の詳細については、次を参照してください。[変更を実行しているドライバー スタック](modifying-a-running-driver-stack.md)します。

これらのイベントの処理を許可する必要がある場合、NDIS は PnP 後の一時停止操作または電源管理の通知を開始できます。 詳細については、次を参照してください。[ドライバー スタックを一時停止](pausing-a-driver-stack.md)します。

 

 





