---
title: システムの電源の変更の処理
description: システムの電源の変更の処理
ms.assetid: 80e36a23-8a41-46f0-a7cb-0039c306a695
keywords:
- 電源は、WDK ネットワークを変更します。
- Nic の WDK ネットワーク、電源のソースの変更
- ネットワーク インターフェイス カード WDK ネットワーク、電源のソースの変更
- プラグ アンド プレイ WDK NDIS ミニポート、電源のソースの変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fec6724de9c670a1c0d7c8974091f7a1c6d31cf7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379830"
---
# <a name="handling-a-change-in-the-systems-power-source"></a>システムの電源の変更の処理





システムは、AC 電源、またはその逆に、バッテリ電源から変更できます。

NDIS ミニポート ドライバーを初期化した後、ミニポート ドライバーが呼び出し[ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)システムの電源のミニポート ドライバーに通知します。 ミニポート ドライバーは、この情報を使用して、NIC の電力消費量を調整するには たとえば、ワイヤレス LAN (WLAN) デバイス用のミニポート ドライバーは、電力消費の削減、システムがバッテリ電源で実行されている場合や、システムが AC 電源で実行されている場合は、電力消費量を増やします。

 

 





