---
title: MiniportDevicePnPEventNotify 関数のエクスポート
description: MiniportDevicePnPEventNotify 関数のエクスポート
ms.assetid: 1c6dce4e-c452-48ce-b3c9-a3fb7842f060
keywords:
- WDK NDIS ミニポートのプラグアンドプレイ、イベント通知
- MiniportDevicePnPEventNotify
- 通知
- 通知 WDK PnP、NDIS ミニポートドライバー
- イベント通知の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e416d8b709f2228280d3f6bce1d009322c6e3ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838111"
---
# <a name="exporting-a-miniportdevicepnpeventnotify-function"></a>MiniportDevicePnPEventNotify 関数のエクスポート





NDIS は、ミニポートドライバーの[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)関数を呼び出して、次のプラグアンドプレイ (PnP) イベントのミニポートドライバーに通知します。

-   ミニポートドライバーで制御される NIC の突然の削除。

-   システムの電源の変更。

ミニポートドライバーで*MiniportDevicePnPEventNotify*関数がエクスポートされない場合、NDIS はこれらの PnP イベントをドライバーに通知できません。

すべての NDIS 6.0 およびそれ以降のミニポートドライバーは、 *MiniportDevicePnPEventNotify*関数をエクスポート*する必要があり*ます。 さらに、WDM が動作しているすべてのミニポートドライバーは、 *MiniportDevicePnPEventNotify*関数をエクスポート*する必要があり*ます。

 

 





