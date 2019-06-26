---
title: SCSI ミニポート ドライバーの HwScsiDisableInterruptsCallback ルーチン
description: SCSI ミニポート ドライバーの HwScsiDisableInterruptsCallback ルーチン
ms.assetid: d6c668cc-cb8d-42f4-a6e0-74bbd8b1b27a
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiDisableInterruptsCallback
- HwScsiDisableInterruptsCallback
- WDK SCSI を中断します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c1c13987a6f392e94bc0ea22ec212ef4289a05e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384323"
---
# <a name="scsi-miniport-drivers-hwscsidisableinterruptscallback-routine"></a>SCSI ミニポート ドライバーの HwScsiDisableInterruptsCallback ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsidisableinterruptscallback_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDISABLEINTERRUPTSCALLBACK_ROUTINE_KG"></span>


[ **HwScsiDisableInterruptsCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557288(v=vs.85))ルーチンは、次を行う必要があります。

-   HBA からの割り込みを再度有効にします。

-   制御を返す

このルーチンが、マシンで他のデバイスの I/O 操作の使用を回避するためにできる限り迅速に実行する必要があることに注意してください。 その結果、 *HwScsiDisableInterruptsCallback*以上のコントロールを返す前に、HBA の割り込みを再度有効にする必要がありますしません。

 

 




