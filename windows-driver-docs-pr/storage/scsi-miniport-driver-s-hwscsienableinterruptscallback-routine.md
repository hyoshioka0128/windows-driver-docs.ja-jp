---
title: SCSI ミニポート ドライバーの HwScsiEnableInterruptsCallback ルーチン
description: SCSI ミニポート ドライバーの HwScsiEnableInterruptsCallback ルーチン
ms.assetid: 8519924f-ad69-46e7-8b24-bf36523f30c9
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiEnableInterruptsCallback
- HwScsiEnableInterruptsCallback
- WDK SCSI を中断します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2edf04c113895c6de6861ed61aa0719063523217
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360183"
---
# <a name="scsi-miniport-drivers-hwscsienableinterruptscallback-routine"></a>SCSI ミニポート ドライバーの HwScsiEnableInterruptsCallback ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsienableinterruptscallback_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIENABLEINTERRUPTSCALLBACK_ROUTINE_KG"></span>


[ **HwScsiEnableInterruptsCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557295(v=vs.85))ルーチンでは、マシンの他のデバイスの I/O 操作を禁止することがなく割り込み駆動の I/O 操作の処理が完了するとします。

ときに、 *HwScsiEnableInterruptsCallback*ルーチン コントロールを取得する、すべてのシステム デバイスの割り込みが有効に以外 HBA からため、 *HwScsiInterrupt*ルーチン HBA の割り込みを無効になっています前に呼び出された[ **ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)します。 したがって、ミニポート ドライバーの*HwScsiInterrupt*ルーチンが呼び出すことはできず、設定するときに現在の操作に関するコンテキスト データを妨害することはできません、 *HwScsiEnableInterruptsCallback*ルーチンは、実行中です。

A *HwScsiEnableInterruptsCallback*ルーチンは、次を行う必要があります。

1.  割り込みの原因となった要求の処理の完了に入力デバイスの拡張機能で操作のために設定されているコンテキストを使用します。

2.  呼び出す**ScsiPortNotification**で、 *NotificationType * * * RequestComplete** だけ満たす SRB とします。

3.  呼び出す**ScsiPortNotification**で、* NotificationType ***NextRequest**、または**NextLuRequest** HBA がタグ付けされたキューまたは論理あたり複数の要求をサポートしている場合単位です。

4.  呼び出す**ScsiPortNotification**デバイス拡張機能へのポインターで、* NotificationType ***CallDisableInterrupts**、および、ミニポート ドライバーの*HwScsiDisableInterruptsCallback*ルーチンを記載[SCSI ミニポート ドライバー HwScsiDisableInterruptsCallback ルーチン](scsi-miniport-driver-s-hwscsidisableinterruptscallback-routine.md)します。

5.  コントロールを返します。

NT ベースのオペレーティング システム**ScsiPortNotification**ルーチンの呼び出し、 *HwScsiDisableInterruptsCallback*ルーチンのシステム デバイスのサブセットに割り込み無効になっています。 HBA の小さいが発生することができます (IRQL) ハードウェアのシステムによって割り当てられた優先度のデバイスの割り込みがありません。

参照してください[IRQL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)詳細についてはします。

 

 




