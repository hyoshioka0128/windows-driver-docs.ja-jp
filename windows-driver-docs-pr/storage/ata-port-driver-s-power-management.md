---
title: ATA ポート ドライバーの電源管理
description: ATA ポート ドライバーの電源管理
ms.assetid: 01c37fed-3b5b-4dd9-bdbd-5c5499a2ddcf
keywords:
- ATA ポート ドライバー WDK、電源管理
- 電源管理の WDK ATA ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41a4ad4b014f058c0e548d16bfcd2ea9b9e2e827
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571331"
---
# <a name="ata-port-drivers-power-management"></a>ATA ポート ドライバーの電源管理


## <span id="ddk_ata_port_drivers_power_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_POWER_MANAGEMENT_KG"></span>


**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。


ATA のポート ドライバーでは、個々 の LUN または個々 のチャネルで電源の状態を変更するミニポート ドライバーを使用します。 LUN の電源の状態を変更する ATA ポート ドライバーに送信、IRB IRB の関数値を持つ\_関数\_POWER\_デバイス ドライバーに変更します。 **PowerChange** IRB のメンバーは、現在を示します。 電源の状態を対象とします。 全体のチャンネルでは、ポート ドライバーの呼び出しの電源状態を変更する、 [ **IdeHwControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557465)ミニポート ドライバー ルーチン。

呼び出すことによって、ミニポート ドライバーが電源の状態遷移を開始できます[ **AtaPortRequestPowerStateChange**](https://msdn.microsoft.com/library/windows/hardware/ff550220)します。 ミニポート ドライバーでは、後に、IDE デバイスのホット プラグでは、このルーチンを呼び出すことができます。

ミニポート ドライバーからのアイドル状態の検出を行うことはお勧めします。

 

 


