---
title: MiniportDevicePnPEventNotify 関数のエクスポート
description: MiniportDevicePnPEventNotify 関数のエクスポート
ms.assetid: 1c6dce4e-c452-48ce-b3c9-a3fb7842f060
keywords:
- プラグ アンド プレイ WDK の NDIS ミニポート、イベント通知
- MiniportDevicePnPEventNotify
- 通知
- WDK PnP、NDIS ミニポート ドライバーの通知
- イベント通知の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca306701c973e56aba974cb88613a32a96eaf667
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373350"
---
# <a name="exporting-a-miniportdevicepnpeventnotify-function"></a>MiniportDevicePnPEventNotify 関数のエクスポート





NDIS ミニポート ドライバーを呼び出す[ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)関数は、次のプラグ アンド プレイ (PnP) イベントのミニポート ドライバーに通知します。

-   ミニポート ドライバーを制御する NIC の突然の削除。

-   システムの電源に変更されました。

ミニポート ドライバーがエクスポートされない場合は、 *MiniportDevicePnPEventNotify*関数は、NDIS ドライバーの PnP これらのイベントを通知できません。

すべての NDIS 6.0 とそれ以降のミニポート ドライバー*する必要があります*エクスポート、 *MiniportDevicePnPEventNotify*関数。 さらに、edge の削減を WDM を持つすべてのミニポート ドライバー*する必要があります*エクスポート、 *MiniportDevicePnPEventNotify*関数。

 

 





