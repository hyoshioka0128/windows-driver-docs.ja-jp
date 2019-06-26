---
title: ミニポート アダプター デバイス PnP イベント通知
description: ミニポート アダプター デバイス PnP イベント通知
ms.assetid: b9417d5d-1f99-480e-8021-e5dd02f28c36
keywords:
- プラグ アンド プレイ WDK ネットワー キング、PnP イベント通知の処理
- ミニポート アダプタの WDK ネットワー キング、プラグ アンド プレイのイベント通知
- アダプターの WDK ネットワー キング、プラグ アンド プレイのイベント通知
- MiniportDevicePnPEventNotify
- イベントの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e55b2190c45a3c91d40ee39eb171fed9b6d68b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373972"
---
# <a name="miniport-adapter-device-pnp-event-notifications"></a>ミニポート アダプター デバイス PnP イベント通知





NDIS ミニポート ドライバーを呼び出す[ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)プラグ アンド プレイ (PnP) イベントのドライバーに通知します。

NDIS PnP イベントを示すイベント コードを提供します。 コードには、アダプターがシステムから予期せず削除されているか、ホスト システムの電源プロファイルが変更されたことを指定できます。

イベントのコードでは、電源プロファイルが変更されたことを示します、NDIS も変更の種類を示します。 システムがバッテリ電源で実行されているか、システムが AC 電源で実行されています。

ミニポート ドライバーはアダプターの設定を調整する必要がありますそれに応じて。

 

 





