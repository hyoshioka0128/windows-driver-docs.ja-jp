---
title: SCSI ミニポート ドライバーの HwScsiTimer ルーチン
description: SCSI ミニポート ドライバーの HwScsiTimer ルーチン
ms.assetid: 57ac7a6e-ada5-4185-89cf-b6c5ef9006d4
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiTimer
- HwScsiTimer
- タイマー WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21b4b2fcbe61e07822dfe67e776dc2d5d3738acb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386494"
---
# <a name="scsi-miniport-drivers-hwscsitimer-routine"></a>SCSI ミニポート ドライバーの HwScsiTimer ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsitimer_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSITIMER_ROUTINE_KG"></span>


ミニポート ドライバーがない、 [ **HwScsiInterrupt** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))ルーチンがすべての HBA の I/O 操作をポーリングして管理するためする必要がありますが、 [ *HwScsiTimer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557327(v=vs.85))ルーチン。 ただし、ミニポート ドライバーが*HwScsiInterrupt*ルーチンが頻繁にある*HwScsiTimer*ルーチンもします。

ミニポート ドライバーを呼び出すことができます、 [ **ScsiPortStallExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportstallexecution)ミニポート ドライバーには、HBA の状態変更の待機、*しない*長く待機するには、このルーチンを呼び出す除く 1 ミリ秒よりも場合によっては、操作の実行、ミニポート ドライバーが初期化のみ。 **ScsiPortStallExecution**一定の間隔でシステムの有用な処理から他のコードを防ぐため、プロセッサと結びついています。

呼び出す代わりに**ScsiPortStallExecution**入力の間隔と多くの CPU サイクルの浪費、ミニポート ドライバーが必要、 *HwScsiTimer*ルーチン。 1 つまたは複数*HwScsiTimer*ルーチンは、HBA がすべての操作の完了の割り込みを生成しない場合、またはバスのリセットなどの操作時間 1 ミリ秒を超えるいずれかのよく要求される場合に特に便利です。

HBA がこのような操作の設定、ミニポート ドライバーは呼び出し[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)で、* NotificationType ***RequestTimerCall**、操作に関するコンテキストを含むその HBA 固有デバイスの拡張機能へのポインター、 *HwScsiTimer*エントリ ポイント、およびドライバーにより決定された間隔。

**ScsiPortNotification**呼び出しを同期して、 *HwScsiTimer*でそれらを日常的な*HwScsiInterrupt*が実行するために日常的なときに同時に、 *HwScsiTimer*ルーチンが実行されています。

*HwScsiTimer*にこのような呼び出しごとに 1 回呼び出されます**ScsiPortNotification**から呼び出すことができ、 *HwScsiTimer*ルーチン自体。 ただし、すべての呼び出しに**ScsiPortNotification**で、 *NotificationType * * * RequestTimerCall** いる、指定した期間が切れていないを呼び出す前に、上書きします。 つまり、ミニポート ドライバーの呼び出しに 1 つだけの未処理の要求がある*HwScsiTimer*特定の時点で日常的な。

渡された間隔**ScsiPortNotification**マイクロ秒単位と各呼び出しのオーバーヘッドの最小値では、 *HwScsiTimer*ルーチンは約 10 (マイクロ秒)。 0 の入力の間隔を呼び出す前の要求をキャンセル、 *HwScsiTimer*ルーチンを提供しないというまたはした SMP の NT ベースのコンピューターの別のプロセッサ上で実行するディスパッチします。

 

 




