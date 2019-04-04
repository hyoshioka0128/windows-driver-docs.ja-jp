---
title: HwScsiInterrupt からの割り込み駆動型 I/O の延期
description: HwScsiInterrupt からの割り込み駆動型 I/O の延期
ms.assetid: 6bedad0c-8995-4c7b-8ee2-415ec63e0eb3
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiInterrupt
- HwScsiInterrupt
- WDK SCSI を中断します。
- 割り込み駆動 I/O WDK SCSI の遅延
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b358d5adf70961f65ebcc04cd52256b9f280ddcd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570450"
---
# <a name="deferring-interrupt-driven-io-from-hwscsiinterrupt"></a>HwScsiInterrupt からの割り込み駆動型 I/O の延期


## <span id="ddk_deferring_interrupt_driven_i_o_from_hwscsiinterrupt_kg"></span><span id="DDK_DEFERRING_INTERRUPT_DRIVEN_I_O_FROM_HWSCSIINTERRUPT_KG"></span>


割り込み駆動の I/O 操作が完了に長時間を受け取らない場合は、ミニポート ドライバーがありますのペア[ **HwScsiEnableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557295)と[ **HwScsiDisableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557288)ルーチン。

たとえば、ミニポート ドライバーが行う PIO、50 マイクロ秒より長く停止する必要があります、 *HwScsiInterrupt*ルーチンにする必要があります*いない*の完全な cpu 使用率を管理完了のポーリング間隔を要求された操作。 代わりに、その*HwScsiInterrupt*ルーチンは、次を行う必要があります。

1.  HBA からの割り込みを無効にします。

2.  操作を完了するために必要な任意のコンテキストで、デバイスの拡張機能を設定します。

3.  呼び出す[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)デバイス拡張機能へのポインターで、* NotificationType ***CallEnableInterrupts**、および、ミニポート ドライバーの*HwScsiEnableInterruptsCallback*ルーチンを記載[SCSI ミニポート ドライバー HwScsiEnableInterruptsCallback ルーチン](scsi-miniport-driver-s-hwscsienableinterruptscallback-routine.md)します。

4.  コントロールを返します。

**ScsiPortNotification**ルーチンの呼び出し、 *HwScsiEnableInterruptsCallback*ルーチンと DPC ルーチン。 Dpc の詳細については、[DPC オブジェクトと Dpc](https://msdn.microsoft.com/library/windows/hardware/ff544084)を参照してください。

ミニポート ドライバーの場合、 *HwScsiInterrupt*ルーチンは、HBA の割り込みを無効にすることはできませんが、その割り込み駆動の転送で 50 を超える (マイクロ秒) を実行できる、 *HwScsiInterrupt*ルーチン、ドライバーライターは、転送を受け入れることのサイズを制限することによって、ミニポート ドライバーを調整する必要があります。 それ以外の場合、マウス ポインターが表示されます「過敏」や、ミニポート ドライバーでは、データを同時に転送が毎回シリアルおよびパラレルのスループットが著しく低下します。

このようなミニポート ドライバーの*HwScsiFindAdapter*ルーチンをリセットする必要があります、 **MaximumTransferLength**ポート値\_構成\_できる値にはその他のシステム ドライバーのパフォーマンスに著しく影響を与えずに割り込み駆動の転送を実行するミニポート ドライバー。

このようなミニポート ドライバーも呼び出すことができます**ScsiPortNotification**ミニポート ドライバーによって提供されると*HwScsiTimer*ルーチン。 詳細については*HwScsiTimer*ルーチンと同期する*HwScsiInterrupt*ルーチンを参照してください[SCSI ミニポート ドライバー HwScsiTimer ルーチン](scsi-miniport-driver-s-hwscsitimer-routine.md)します。

 

 




