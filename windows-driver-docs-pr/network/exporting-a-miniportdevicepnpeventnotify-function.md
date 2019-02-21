---
title: MiniportDevicePnPEventNotify 関数をエクスポートします。
description: MiniportDevicePnPEventNotify 関数をエクスポートします。
ms.assetid: 1c6dce4e-c452-48ce-b3c9-a3fb7842f060
keywords:
- プラグ アンド プレイ WDK の NDIS ミニポート、イベント通知
- MiniportDevicePnPEventNotify
- 通知
- WDK PnP、NDIS ミニポート ドライバーの通知
- イベント通知の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8398ab93e6ab9208cc25954ba94a9575cccd5e73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548596"
---
# <a name="exporting-a-miniportdevicepnpeventnotify-function"></a>MiniportDevicePnPEventNotify 関数をエクスポートします。





NDIS ミニポート ドライバーを呼び出す[ *MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)関数は、次のプラグ アンド プレイ (PnP) イベントのミニポート ドライバーに通知します。

-   ミニポート ドライバーを制御する NIC の突然の削除。

-   システムの電源に変更されました。

ミニポート ドライバーがエクスポートされない場合は、 *MiniportDevicePnPEventNotify*関数は、NDIS ドライバーの PnP これらのイベントを通知できません。

すべての NDIS 6.0 とそれ以降のミニポート ドライバー*する必要があります*エクスポート、 *MiniportDevicePnPEventNotify*関数。 さらに、edge の削減を WDM を持つすべてのミニポート ドライバー*する必要があります*エクスポート、 *MiniportDevicePnPEventNotify*関数。

 

 





