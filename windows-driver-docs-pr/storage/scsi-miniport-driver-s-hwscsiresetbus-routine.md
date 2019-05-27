---
title: SCSI ミニポート ドライバーの HwScsiResetBus ルーチン
description: SCSI ミニポート ドライバーの HwScsiResetBus ルーチン
ms.assetid: ca4ab3e6-e23c-443a-bcf6-6fd516569999
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiResetBus
- HwScsiResetBus
- WDK SCSI バスのリセットの操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9690e30a1a4169914e62fab843ca086add012fb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378952"
---
# <a name="scsi-miniport-drivers-hwscsiresetbus-routine"></a>SCSI ミニポート ドライバーの HwScsiResetBus ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiresetbus_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIRESETBUS_ROUTINE_KG"></span>


すべてのミニポート ドライバーが必要、 [ *HwScsiResetBus* ](https://msdn.microsoft.com/library/windows/hardware/ff557318) HBA の状態のミニポート ドライバーのデバイスの拡張機能へのポインターと呼ばれる、ルーチン、 **PathId**のリセットするバスです。 試行のバスのリセット操作では、障害が発生したり、タイムアウト、ミニポート ドライバーを呼び出す必要があります[ **ScsiPortLogError** ](https://msdn.microsoft.com/library/windows/hardware/ff564652)とし、ハード リセットの HBA をプログラムします。

バスのリセット操作には、デバイスの拡張機能や、バス上のデバイスの論理ユニットの拡張機能内で管理状態をクリーンアップするミニポート ドライバーを必要があります。 *HwScsiResetBus*呼び出すことにより、未処理の要求を完了する必要があります[ **ScsiPortCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff564608)で、 **SrbStatus**値 SRB\_状態\_BUS\_リセットまたは個々 のされる Srb [ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)この状態値。

バスのリセット要求と、未処理の要求を完了すると、ミニポート ドライバーを呼び出す必要があります**ScsiPortNotification** (これがまだ行っていない) 場合に、* NotificationType \* **NextRequest**、または **NextLuRequest** HBA がタグ付けされたキューまたは論理ユニットごとの複数の要求をサポートしている場合。

オペレーティング システム - 特定のポートのドライバーがミニポート ドライバーに代わって SCSI バスのリセットの遅延を管理するに注意してください。

 

 




