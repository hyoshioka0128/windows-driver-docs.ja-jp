---
title: SCSI ミニポート ドライバーの HwScsiResetBus ルーチン
description: SCSI ミニポート ドライバーの HwScsiResetBus ルーチン
ms.assetid: ca4ab3e6-e23c-443a-bcf6-6fd516569999
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiResetBus
- HwScsiResetBus
- バスリセット操作 (WDK SCSI)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96e53ffddf35142195f6ec74f62608e7190420d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842664"
---
# <a name="scsi-miniport-drivers-hwscsiresetbus-routine"></a>SCSI ミニポート ドライバーの HwScsiResetBus ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiresetbus_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIRESETBUS_ROUTINE_KG"></span>


すべてのミニポートドライバーには[*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))ルーチンが必要です。これは、HBA 状態のミニポートドライバーのデバイス拡張機能へのポインターと、リセットするバスの**PathId**を使用して呼び出されます。 バスリセット操作の試行が失敗した場合、またはタイムアウトになった場合、ミニポートドライバーは[**ScsiPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportlogerror)を呼び出して、ハードリセットのために HBA をプログラムする必要があります。

バスリセット操作では、ミニポートドライバーが、バス上のデバイスのデバイス拡張機能または論理ユニット拡張機能によって保持されている状態をクリーンアップすることが必要になる場合があります。 *HwScsiResetBus*は、 [**ScsiPortCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportcompleterequest)を呼び出すことによって未処理の要求を完了する必要があります。これには、 **srbstatus**値 SRB\_STATUS\_BUS\_RESET を使用するか、個々の SRBs, [**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)に対してを呼び出しますこの状態値を持つ。

バスリセット要求と未処理の要求が完了すると、ミニポートドライバーは、* NotificationType ***nextrequest**または**NEXTLUREQUEST** (HBA がサポートしている場合) を使用して、 **ScsiPortNotification** (まだ完了していない場合) を呼び出す必要があります。1つの論理ユニットにつきキューまたは複数の要求をタグ付けします。

オペレーティングシステム固有のポートドライバーでは、ミニポートドライバーに代わって SCSI バスリセットの遅延が管理されることに注意してください。

 

 




