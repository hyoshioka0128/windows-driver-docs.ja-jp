---
title: ATA ポート ドライバーの電源管理
description: ATA ポート ドライバーの電源管理
ms.assetid: 01c37fed-3b5b-4dd9-bdbd-5c5499a2ddcf
keywords:
- ATA ポート ドライバー WDK、電源管理
- 電源管理の WDK ATA ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f546e74df025fd1829699539d492124b891c1cf0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368418"
---
# <a name="ata-port-drivers-power-management"></a>ATA ポート ドライバーの電源管理


## <span id="ddk_ata_port_drivers_power_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_POWER_MANAGEMENT_KG"></span>


**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。


ATA のポート ドライバーでは、個々 の LUN または個々 のチャネルで電源の状態を変更するミニポート ドライバーを使用します。 LUN の電源の状態を変更する ATA ポート ドライバーに送信、IRB IRB の関数値を持つ\_関数\_POWER\_デバイス ドライバーに変更します。 **PowerChange** IRB のメンバーは、現在を示します。 電源の状態を対象とします。 全体のチャンネルでは、ポート ドライバーの呼び出しの電源状態を変更する、 [ **IdeHwControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_control)ミニポート ドライバー ルーチン。

呼び出すことによって、ミニポート ドライバーが電源の状態遷移を開始できます[ **AtaPortRequestPowerStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportrequestpowerstatechange)します。 ミニポート ドライバーでは、後に、IDE デバイスのホット プラグでは、このルーチンを呼び出すことができます。

ミニポート ドライバーからのアイドル状態の検出を行うことはお勧めします。

 

 


