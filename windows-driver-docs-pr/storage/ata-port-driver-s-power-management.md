---
title: ATA ポート ドライバーの電源管理
description: ATA ポート ドライバーの電源管理
ms.assetid: 01c37fed-3b5b-4dd9-bdbd-5c5499a2ddcf
keywords:
- ATA ポートドライバー WDK、電源管理
- 電源管理 WDK ATA ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d552f08e5f3d649d86f24cf232626386bb8bf2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845104"
---
# <a name="ata-port-drivers-power-management"></a>ATA ポート ドライバーの電源管理


## <span id="ddk_ata_port_drivers_power_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_POWER_MANAGEMENT_KG"></span>


**メモ**ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。


ATA ポートドライバーを使用すると、ミニポートドライバーで個々の LUN または個々のチャネルの電源状態を変更できます。 LUN の電源状態を変更するために、ATA ポートドライバーは IRB\_関数の関数値を使用して IRB を送信し\_電源\_デバイスドライバーに変更します。 IRB の**Powerchange**メンバーは、現在の電源状態とターゲットの電源状態を示します。 チャネル全体の電源状態を変更するために、ポートドライバーは[**IdeHwControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_control)ミニポートドライバールーチンを呼び出します。

ミニポートドライバーは、 [**AtaPortRequestPowerStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportrequestpowerstatechange)を呼び出すことによって電源状態の移行を開始できます。 ミニポートドライバーは、たとえば IDE デバイスのホットプラグの後に、このルーチンを呼び出す場合があります。

ミニポートドライバーからアイドル状態の検出を行うことは推奨されません。

 

 


