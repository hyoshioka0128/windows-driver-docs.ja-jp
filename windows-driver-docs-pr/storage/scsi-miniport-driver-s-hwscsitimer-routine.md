---
title: SCSI ミニポート ドライバーの HwScsiTimer ルーチン
description: SCSI ミニポート ドライバーの HwScsiTimer ルーチン
ms.assetid: 57ac7a6e-ada5-4185-89cf-b6c5ef9006d4
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiTimer
- HwScsiTimer
- タイマー WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59a327103c9cb2151a27724e357b28089f8621cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842660"
---
# <a name="scsi-miniport-drivers-hwscsitimer-routine"></a>SCSI ミニポート ドライバーの HwScsiTimer ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsitimer_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSITIMER_ROUTINE_KG"></span>


ポーリングによってすべての HBA i/o 操作を管理するため、 [**HwScsiInterrupt**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))ルーチンを持たないミニポートドライバーには[*HwScsiTimer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557327(v=vs.85))ルーチンが必要です。 ただし、 *HwScsiInterrupt*ルーチンを使用するミニポートドライバーにも、多くの場合、 *HwScsiTimer*ルーチンがあります。

ミニポートドライバーは[**ScsiPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportstallexecution)を呼び出して HBA の状態の変化を待機することができますが、ミニポートドライバーはこのルーチンを呼び出して、1ミリ秒以上待機することはでき*ません*。ただし、ミニポートドライバーを初期化しています。 **ScsiPortStallExecution**は、指定された間隔でプロセッサを関連付け、システム内の他のコードが有用な作業を実行できないようにします。

大きな入力間隔で**ScsiPortStallExecution**を呼び出し、多くの CPU サイクルを浪費するのではなく、ミニポートドライバーに*HwScsiTimer*ルーチンが必要です。 1つ以上の*HwScsiTimer*ルーチンは、HBA がすべての操作に対して完了割り込みを生成しない場合、またはバスのリセットなどの一般的に要求される操作がミリ秒より長くかかる場合に特に便利です。

このような操作に対して HBA がプログラムされた後、ミニポートドライバーは、* NotificationType ***Requesttimercall**、その操作に関するコンテキストを含む hba 固有のデバイス拡張機能へのポインターを使用して[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)を呼び出します。*HwScsiTimer*エントリポイント、およびドライバーによって決定された間隔。

**ScsiPortNotification**は、 *HwScsiTimer*ルーチンと*HwScsiInterrupt*ルーチンの呼び出しを同期して、 *HwScsiTimer*ルーチンの実行中に同時に実行できないようにします。

*HwScsiTimer*は、 **ScsiPortNotification**の呼び出しごとに1回呼び出されます。これは、 *HwScsiTimer*ルーチン自体から呼び出すことができます。 ただし、 *NotificationType * * * RequestTimerCall** を使用して**ScsiPortNotification**を呼び出すと、指定した時間が経過していない前の呼び出しが上書きされます。 つまり、特定の時点でミニポートドライバーの*HwScsiTimer*ルーチンを呼び出すための未処理の要求は1つだけです。

**ScsiPortNotification**に渡される間隔はマイクロ秒単位であり、 *HwScsiTimer*ルーチンの各呼び出しの最小オーバーヘッドは約10マイクロ秒です。 入力間隔が0の場合、 *HwScsiTimer*ルーチンを呼び出すために、前の要求が取り消されます。これは、NT ベースの SMP マシンの別のプロセッサで実行するために呼び出されなかったか、ディスパッチされていない場合に発生します。

 

 




