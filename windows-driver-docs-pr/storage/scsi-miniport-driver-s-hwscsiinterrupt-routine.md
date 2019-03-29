---
title: SCSI ミニポート ドライバーの HwScsiInterrupt ルーチン
description: SCSI ミニポート ドライバーの HwScsiInterrupt ルーチン
ms.assetid: 8760e7e4-1721-4e55-99e6-c9e234368fa1
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiInterrupt
- HwScsiInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 044e7e95950cd724feda8b59eb1ca47256fcec0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573343"
---
# <a name="scsi-miniport-drivers-hwscsiinterrupt-routine"></a>SCSI ミニポート ドライバーの HwScsiInterrupt ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiinterrupt_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINTERRUPT_ROUTINE_KG"></span>


開始時、 [ **HwScsiInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff557312)ルーチンがその HBA が実際に割り込みを生成したかどうかを決定する必要があります。 *HwScsiInterrupt*返す必要があります**FALSE**実際には、割り込みを生成したデバイスの ISR を簡単に呼び出すことができるように、不正な割り込みが検出された場合に、できるだけ早くします。

それ以外の場合、ミニポート ドライバーの*HwScsiInterrupt*ルーチンは通常、割り込みの原因となった I/O 操作を完了する責任を負います。 HBA およびミニポート ドライバーの設計によって、 *HwScsiInterrupt*ルーチンは、次の一部またはすべて。

-   (必須)、HBA の割り込みを閉じる

-   ポート ドライバーに通知 (呼び出して[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)または[ **ScsiPortCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff564608))、HBA が示す場合特定の SCSI エラー条件では、操作中に発生し、エラーを記録する可能性があります。

    エラーのログ記録の詳細については、次を参照してください。 [SCSI ミニポート ドライバーのエラー処理](error-handling-in-scsi-miniport-drivers.md)します。

-   呼び出しなど、割り込みの原因となった、要求された操作が完了すると[ **ScsiPortIoMapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff564649) (を参照してください[SCSI ミニポート ドライバー HwScsiDmaStarted ルーチン](scsi-miniport-driver-s-hwscsidmastarted-routine.md)) 場合割り込み元以前に選択したターゲット TID と LU、データを転送する準備ができることを示します。

ときに、 *HwScsiInterrupt*ルーチン (または内部のミニポート ドライバーのルーチン)、SRB が完了すると、呼び出す**ScsiPortNotification** 2 回。

1.  最初に、 *NotificationType * * * RequestComplete** だけ満たす SRB とします。

2.  次で、* NotificationType ***NextRequest**、または**NextLuRequest** HBA がタグ付けされたキューまたは論理ユニットごとの複数の要求をサポートしている場合。

全体的なシステム パフォーマンスを向上させる、ミニポート ドライバーの*HwScsiInterrupt*ルーチンが I/O 要求の処理に必要な最小のみを行う必要があります。 制御を返す、ミニポート ドライバーを設計することは、 *HwScsiInterrupt*できる限り迅速に日常的な。 *HwScsiInterrupt*ルーチンを呼び出してはならない[ **ScsiPortStallExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff564757) 、大規模な間隔でプロセッサを独占されと他のドライバーからの防止デバイスの割り込みです。

 

 




