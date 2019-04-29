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
ms.openlocfilehash: 8398ab93e6ab9208cc25954ba94a9575cccd5e73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385486"
---
# <a name="exporting-a-miniportdevicepnpeventnotify-function"></a>MiniportDevicePnPEventNotify 関数のエクスポート





NDIS ミニポート ドライバーを呼び出す[ *MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)関数は、次のプラグ アンド プレイ (PnP) イベントのミニポート ドライバーに通知します。

-   ミニポート ドライバーを制御する NIC の突然の削除。

-   システムの電源に変更されました。

ミニポート ドライバーがエクスポートされない場合は、 *MiniportDevicePnPEventNotify*関数は、NDIS ドライバーの PnP これらのイベントを通知できません。

すべての NDIS 6.0 とそれ以降のミニポート ドライバー*する必要があります*エクスポート、 *MiniportDevicePnPEventNotify*関数。 さらに、edge の削減を WDM を持つすべてのミニポート ドライバー*する必要があります*エクスポート、 *MiniportDevicePnPEventNotify*関数。

 

 





