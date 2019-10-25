---
title: SCSI ミニポート ドライバーの HwScsiInterrupt ルーチン
description: SCSI ミニポート ドライバーの HwScsiInterrupt ルーチン
ms.assetid: 8760e7e4-1721-4e55-99e6-c9e234368fa1
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiInterrupt
- HwScsiInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32755817e01e3ab720512ced49d9f9708afe5fbc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842666"
---
# <a name="scsi-miniport-drivers-hwscsiinterrupt-routine"></a>SCSI ミニポート ドライバーの HwScsiInterrupt ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiinterrupt_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINTERRUPT_ROUTINE_KG"></span>


エントリでは、 [**HwScsiInterrupt**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))ルーチンは、HBA が実際に割り込みを生成したかどうかを判断する必要があります。 *HwScsiInterrupt*は、誤った割り込みが検出された場合、できるだけ早く**FALSE**を返す必要があるため、割り込みを実際に生成したデバイスの ISR を迅速に呼び出すことができます。

それ以外の場合は、通常、ミニポートドライバーの*HwScsiInterrupt*ルーチンが、割り込みの原因となった i/o 操作の完了を担当します。 HBA とミニポートドライバーの設計に応じて、 *HwScsiInterrupt*ルーチンは次の一部またはすべてを実行します。

-   HBA の割り込みを破棄します (必須)

-   操作中に特定の SCSI エラー状態が発生したことが HBA に示され、場合によってはエラーがログに記録される場合は、 [**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)または[**ScsiPortCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportcompleterequest)を呼び出すことによって、ポートドライバーに通知します。

    ログエラーの詳細については、「 [SCSI ミニポートドライバーでのエラー処理](error-handling-in-scsi-miniport-drivers.md)」を参照してください。

-   割り込みの原因となった要求された操作を完了します。たとえば、以前に選択されたターゲット TID と LU から割り込みが発生した場合は、 [**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer)を呼び出します ( [SCSI ミニポートドライバーの HwScsiDmaStarted ルーチン](scsi-miniport-driver-s-hwscsidmastarted-routine.md)を参照してください)。データ転送の準備。

*HwScsiInterrupt*ルーチン (または内部ミニポートドライバールーチン) が SRB を完了すると、 **ScsiPortNotification**を2回呼び出します。

1.  1つ目は、 *NotificationType * * * RequestComplete** と、それだけが満たされた SRB です。

2.  次に、* NotificationType ***Nextrequest**を使用するか、HBA がタグ付きキューまたは複数の要求を論理ユニットごとにサポートする場合は、 **nextlurequest**を使用します。

システム全体のパフォーマンスを向上させるために、ミニポートドライバーの*HwScsiInterrupt*ルーチンは、i/o 要求を処理するために必要な最小要件のみを実行する必要があります。 つまり、ミニポートドライバーは、できるだけ早く*HwScsiInterrupt*ルーチンから制御を返すように設計する必要があります。 *HwScsiInterrupt*ルーチンは、長い間隔で[**ScsiPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportstallexecution)を呼び出さないでください。これにより、プロセッサを独占し、他のドライバーがそのデバイスの割り込みを処理するのを防ぐことができます。

 

 




