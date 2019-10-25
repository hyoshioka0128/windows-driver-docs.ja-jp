---
title: オーディオ デバイスの電源管理
description: オーディオ デバイスの電源管理
ms.assetid: 3d3d63af-5790-4760-9099-7116ed5a5446
keywords:
- オーディオドライバー WDK、電源管理
- オーディオミニポートドライバー WDK、電源管理
- ミニポートドライバー WDK オーディオ、電源管理
- 電源管理 WDK オーディオ
- ポートクラスドライバー WDK オーディオ
- PortCls WDK audio, 電源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9033d591856c156b7918d11714a781a0f869b0c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830231"
---
# <a name="power-management-for-audio-devices"></a>オーディオ デバイスの電源管理


## <span id="power_management_for_audio_devices"></span><span id="POWER_MANAGEMENT_FOR_AUDIO_DEVICES"></span>


PortCls システムドライバーは、オーディオアダプタードライバーに代わって、すべての電源管理の Irp を処理します (「[電源 irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-power-irps)」を参照してください)。 PortCls は、アダプタードライバーの[Iadapterpowermanagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement)インターフェイスと[ipowernotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-ipowernotify)インターフェイスを使用して呼び出しを行うことによって、オーディオデバイスの電源状態を管理します。 どちらのインターフェイスも省略可能です。 PortCls からの要求に応答して電源状態を変更できるデバイスのアダプタードライバーは、IAdapterPowerManagement インターフェイスを公開する必要があります。 差し迫った電源の警告を必要とするミニポートオブジェクトは、IPowerNotify インターフェイスを公開する必要があります。

Windows Server 2003 SP1、Windows XP SP2、およびそれ以降では、PortCls はタイマーを使用して、指定されたタイムアウト期間内に非アクティブの状態になっているオーディオデバイスの電源を切るタイミングを決定します。 PortCls は、タイムアウト間隔と、タイムアウトが発生したときのターゲットの電源状態の既定値を提供します。 ハードウェアベンダーは、必要に応じて、独自のドライバー固有の値を使用してこれらの既定値を上書きできます。

このセクションでは、次のトピックについて説明します。

[IAdapterPowerManagement の実装](implementing-iadapterpowermanagement.md)

[IPowerNotify の実装](implementing-ipowernotify.md)

[オーディオデバイスクラスの非アクティブタイマーの実装](audio-device-class-inactivity-timer-implementation.md)

 

 




