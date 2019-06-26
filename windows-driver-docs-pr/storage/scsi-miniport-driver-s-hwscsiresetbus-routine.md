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
ms.openlocfilehash: 2e0ebbcaed5e40fb1bededeac1499e169c35f273
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385219"
---
# <a name="scsi-miniport-drivers-hwscsiresetbus-routine"></a>SCSI ミニポート ドライバーの HwScsiResetBus ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiresetbus_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIRESETBUS_ROUTINE_KG"></span>


すべてのミニポート ドライバーが必要、 [ *HwScsiResetBus* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85)) HBA の状態のミニポート ドライバーのデバイスの拡張機能へのポインターと呼ばれる、ルーチン、 **PathId**のリセットするバスです。 試行のバスのリセット操作では、障害が発生したり、タイムアウト、ミニポート ドライバーを呼び出す必要があります[ **ScsiPortLogError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportlogerror)とし、ハード リセットの HBA をプログラムします。

バスのリセット操作には、デバイスの拡張機能や、バス上のデバイスの論理ユニットの拡張機能内で管理状態をクリーンアップするミニポート ドライバーを必要があります。 *HwScsiResetBus*呼び出すことにより、未処理の要求を完了する必要があります[ **ScsiPortCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportcompleterequest)で、 **SrbStatus**値 SRB\_状態\_BUS\_リセットまたは個々 のされる Srb [ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)この状態値。

バスのリセット要求と、未処理の要求を完了すると、ミニポート ドライバーを呼び出す必要があります**ScsiPortNotification** (これがまだ行っていない) 場合に、*NotificationType* **NextRequest**、または **NextLuRequest** HBA がタグ付けされたキューまたは論理ユニットごとの複数の要求をサポートしている場合。

オペレーティング システム - 特定のポートのドライバーがミニポート ドライバーに代わって SCSI バスのリセットの遅延を管理するに注意してください。

 

 




