---
title: ミニポート アダプター デバイス PnP イベント通知
description: ミニポート アダプター デバイス PnP イベント通知
ms.assetid: b9417d5d-1f99-480e-8021-e5dd02f28c36
keywords:
- WDK ネットワークのプラグアンドプレイ、PnP イベント通知の処理
- ミニポートアダプター WDK ネットワーク、プラグアンドプレイイベント通知
- WDK ネットワークのアダプター、プラグアンドプレイイベント通知
- MiniportDevicePnPEventNotify
- イベント WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8a9dda1cd5069dc5cbbd6b83df613dca753bbf2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844256"
---
# <a name="miniport-adapter-device-pnp-event-notifications"></a>ミニポート アダプター デバイス PnP イベント通知





NDIS は、ミニポートドライバーの[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)関数を呼び出して、ドライバープラグアンドプレイ (PnP) イベントを通知します。

NDIS には、PnP イベントを説明するイベントコードが用意されています。 このコードは、アダプターがシステムから予期せず削除されたこと、またはホストシステムの電源プロファイルが変更されたことを示している可能性があります。

イベントコードによって電源プロファイルが変更されたことが示された場合は、NDIS によって変更の種類も示されます。 システムがバッテリ電源で動作しているか、システムが AC 電源で実行されています。

ミニポートドライバーは、それに応じてアダプターの設定を調整する必要があります。

 

 





