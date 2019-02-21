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
ms.openlocfilehash: b1e68925623965c7686d434c9b76faaf46602bd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527680"
---
# <a name="miniport-adapter-device-pnp-event-notifications"></a>ミニポート アダプター デバイス PnP イベント通知





NDIS ミニポート ドライバーを呼び出す[ *MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)プラグ アンド プレイ (PnP) イベントのドライバーに通知します。

NDIS PnP イベントを示すイベント コードを提供します。 コードには、アダプターがシステムから予期せず削除されているか、ホスト システムの電源プロファイルが変更されたことを指定できます。

イベントのコードでは、電源プロファイルが変更されたことを示します、NDIS も変更の種類を示します。 システムがバッテリ電源で実行されているか、システムが AC 電源で実行されています。

ミニポート ドライバーはアダプターの設定を調整する必要がありますそれに応じて。

 

 





