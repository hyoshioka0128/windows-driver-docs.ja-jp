---
title: SCSI ミニポート ドライバーの HwScsiEnableInterruptsCallback ルーチン
description: SCSI ミニポート ドライバーの HwScsiEnableInterruptsCallback ルーチン
ms.assetid: 8519924f-ad69-46e7-8b24-bf36523f30c9
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiEnableInterruptsCallback
- HwScsiEnableInterruptsCallback
- WDK SCSI の割り込み
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 87159bbebfd343e7f285a7b383527b87ddef593e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842672"
---
# <a name="scsi-miniport-drivers-hwscsienableinterruptscallback-routine"></a>SCSI ミニポート ドライバーの HwScsiEnableInterruptsCallback ルーチン

[*HwScsiEnableInterruptsCallback*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557295(v=vs.85))ルーチンは、マシン内の他のデバイスに対して損なわれる i/o 操作を行わずに、割り込みドリブン i/o 操作の処理を終了します。

*HwScsiEnableInterruptsCallback*ルーチンが制御を取得すると、hba を除くすべてのシステムデバイスの割り込みが有効になります。これは、 *HWSCSIINTERRUPT*ルーチンが hba の割り込みを無効にしてから [**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) を呼び出したためです。 このため、ミニポートドライバーの*HwScsiInterrupt*ルーチンを呼び出すことはできません。また、 *HwScsiEnableInterruptsCallback*ルーチンの実行中に、現在の操作について設定されているコンテキストデータを応答することはできません。

*HwScsiEnableInterruptsCallback*ルーチンは、次の操作を行う必要があります。

1. 割り込みの原因となった要求の処理を完了するために、入力デバイス拡張機能の操作用に設定されたコンテキストを使用します。

2. *NotificationType * ** * **ScsiPortNotification** * を使用して呼び出し、SRB を満たしていることを確認します。

3. **ScsiPortNotification**を、* NotificationType ***nextrequest**を使用して呼び出すか、HBA がタグ付きキューまたは複数の要求を論理ユニットごとにサポートする場合は、 **nextlurequest**を呼び出します。

4. 「 SCSI ミニポートドライバー」で説明されているように、デバイス拡張機能へのポインター、* NotificationType ***calldisableinterrupts**、およびミニポートドライバーの*HwScsiDisableInterruptsCallback*ルーチンを使用して ScsiPortNotification を呼び出します。 [HwScsiDisableInterruptsCallback ルーチン](scsi-miniport-driver-s-hwscsidisableinterruptscallback-routine.md)。

5. 制御を返します。

NT ベースのオペレーティングシステムの**ScsiPortNotification**ルーチンは、無効になっているシステムデバイス割り込みのサブセットを使用して*HwScsiDisableInterruptsCallback*ルーチンを呼び出します。 システムによって割り当てられたハードウェア優先度 (IRQL) が HBA 以下であるデバイスの割り込みが発生することはありません。

詳細については、「[ハードウェアの優先順位の管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities
)」を参照してください。
