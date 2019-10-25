---
title: システムの電源の変更の処理
description: システムの電源の変更の処理
ms.assetid: 80e36a23-8a41-46f0-a7cb-0039c306a695
keywords:
- power source の WDK ネットワークの変更
- Nic WDK ネットワーク、電源ソースの変更
- ネットワークインターフェイスカード WDK ネットワーク、電源ソースの変更
- WDK NDIS ミニポートのプラグアンドプレイ、電源の変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c24cb49f705d3ac9c7f3f7df3bdf77cc52fe0e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842116"
---
# <a name="handling-a-change-in-the-systems-power-source"></a>システムの電源の変更の処理





システムは、バッテリ電源、AC 電源、またはその逆に変化することがあります。

ミニポートドライバーを初期化した後、NDIS はミニポートドライバーの[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)関数を呼び出して、システムの電源のミニポートドライバーに通知します。 ミニポートドライバーは、この情報を使用して NIC の電力消費を調整できます。 たとえば、ワイヤレス LAN (WLAN) デバイス用のミニポートドライバーにより、システムがバッテリ電源で動作している場合は電力消費が減少し、システムが AC 電源で実行されている場合は電力消費が増加する可能性があります。

 

 





