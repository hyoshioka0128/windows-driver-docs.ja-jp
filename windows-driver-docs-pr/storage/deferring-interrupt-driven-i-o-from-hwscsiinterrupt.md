---
title: HwScsiInterrupt からの割り込み駆動型 I/O の延期
description: HwScsiInterrupt からの割り込み駆動型 I/O の延期
ms.assetid: 6bedad0c-8995-4c7b-8ee2-415ec63e0eb3
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiInterrupt
- HwScsiInterrupt
- WDK SCSI の割り込み
- 遅延割り込みドリブン i/o (WDK SCSI)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc7bb3dd4063d596d69b27d9224a9c6d8a42ddc9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845189"
---
# <a name="deferring-interrupt-driven-io-from-hwscsiinterrupt"></a>HwScsiInterrupt からの割り込み駆動型 I/O の延期


## <span id="ddk_deferring_interrupt_driven_i_o_from_hwscsiinterrupt_kg"></span><span id="DDK_DEFERRING_INTERRUPT_DRIVEN_I_O_FROM_HWSCSIINTERRUPT_KG"></span>


割り込みドリブン i/o 操作が完了するまでに時間がかかる場合、ミニポートドライバーには[**HwScsiEnableInterruptsCallback**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557295(v=vs.85))ルーチンと[**HwScsiDisableInterruptsCallback**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557288(v=vs.85))ルーチンのペアが必要です。

たとえば、ミニポートドライバーが PIO を実行する50マイクロ秒を超えて停止する必要がある場合、その*HwScsiInterrupt*ルーチンは、要求された操作を完了するために、完全なポーリング間隔の CPU の制御を保持し*ない*ようにする必要があります。 代わりに、 *HwScsiInterrupt*ルーチンは次のことを行う必要があります。

1.  HBA からの割り込みを無効にします。

2.  操作を完了するために必要なコンテキストでデバイス拡張機能を設定します。

3.  「 [SCSI ミニポートドライバーの HwScsiEnableInterruptsCallback ルーチン](scsi-miniport-driver-s-hwscsienableinterruptscallback-routine.md)」で説明されているように、デバイス拡張機能、* NotificationType ***callenableinterrupts**、およびミニポートドライバーの*HwScsiEnableInterruptsCallback*ルーチンへのポインターを使用して、 [**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)を呼び出します。

4.  制御を返します。

**ScsiPortNotification**ルーチンは、DPC ルーチンとして*HwScsiEnableInterruptsCallback*ルーチンを呼び出します。 Dpc の詳細については、「 [Dpc オブジェクトと](https://docs.microsoft.com/windows-hardware/drivers/kernel/dpc-objects-and-dpcs)dpc」を参照してください。

ミニポートドライバーの*HwScsiInterrupt*ルーチンで、HBA の割り込みを無効にできないが、割り込みドリブン転送が*HwScsiInterrupt*ルーチンで50マイクロ秒を超える可能性がある場合、ドライバーライターはミニポートドライバーを許容される転送のサイズを制限する。 そうしないと、マウスポインターが "過敏" と表示されます。または、ミニポートドライバーがデータを同時に転送するたびに、並列スループットが著しく低下します。

このようなミニポートドライバーの*HwScsiFindAdapter*ルーチンは、ポート\_構成\_情報の**maximumtransferlength**値を、ミニポートドライバーが割り込み駆動の転送を実行できるようにする値にリセットする必要があります。他のシステムドライバーのパフォーマンスに大きな影響を与えることはありません。

このようなミニポートドライバーは、ミニポートドライバーが提供する*HwScsiTimer*ルーチンを使用して**ScsiPortNotification**を呼び出すこともできます。 *HwScsiInterrupt*ルーチンと同期される*HwScsiTimer*ルーチンの詳細については、「 [SCSI ミニポートドライバーの HwScsiTimer ルーチン](scsi-miniport-driver-s-hwscsitimer-routine.md)」を参照してください。

 

 




