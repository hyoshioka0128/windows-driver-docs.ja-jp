---
title: オーディオ デバイスの電源管理
description: オーディオ デバイスの電源管理
ms.assetid: 3d3d63af-5790-4760-9099-7116ed5a5446
keywords:
- オーディオ ドライバー WDK、電源管理
- オーディオのミニポート ドライバー WDK、電源管理
- ミニポート ドライバー WDK オーディオ、電源管理
- 電源管理の WDK オーディオ
- ポート クラス ドライバー WDK オーディオ
- PortCls WDK オーディオ、電源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf895a8ad46f8429acef523b094d6d1d24a03d46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362543"
---
# <a name="power-management-for-audio-devices"></a>オーディオ デバイスの電源管理


## <span id="power_management_for_audio_devices"></span><span id="POWER_MANAGEMENT_FOR_AUDIO_DEVICES"></span>


PortCls システムのドライバーすべての電源管理 Irp の処理 (を参照してください[Power Irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-power-irps)) オーディオ アダプター ドライバーの代わりです。 PortCls アダプター ドライバーの使用を呼び出すことで、オーディオ デバイスの電源状態を管理する[IAdapterPowerManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement)と[IPowerNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipowernotify)インターフェイス。 両方のインターフェイスは省略可能です。 PortCls からの要求に応答の電源状態を変更できるデバイスのドライバーでは、IAdapterPowerManagement インターフェイスを公開する必要があります。 事前に警告の兆候の電源切断を必要とするミニポート オブジェクトには、IPowerNotify インターフェイスを公開する必要があります。

Windows Server 2003 SP1、Windows XP SP2 で PortCls はタイマーを使用して、電源を切るオーディオ デバイスによって指定されたタイムアウト時間の非アクティブなままであった場合の判別を後と。 PortCls では、タイムアウトが発生したときに、タイムアウト間隔と対象の電源状態の既定値を提供します。 ハードウェア ベンダーは、独自のドライバー固有の値を持つこれらの既定値を必要に応じて上書きできます。

このセクションでは、次のトピックについて説明します。

[IAdapterPowerManagement を実装します。](implementing-iadapterpowermanagement.md)

[IPowerNotify を実装します。](implementing-ipowernotify.md)

[オーディオ デバイス クラスの非アクティブ タイマーの実装](audio-device-class-inactivity-timer-implementation.md)

 

 




