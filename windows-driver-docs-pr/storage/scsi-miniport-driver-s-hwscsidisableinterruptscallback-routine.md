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
ms.openlocfilehash: 6713a8cf8932467aec5c612c9f6b826a9520fb0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539695"
---
# <a name="scsi-miniport-drivers-hwscsidisableinterruptscallback-routine"></a>SCSI ミニポート ドライバーの HwScsiDisableInterruptsCallback ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsidisableinterruptscallback_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDISABLEINTERRUPTSCALLBACK_ROUTINE_KG"></span>


[ **HwScsiDisableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557288)ルーチンは、次を行う必要があります。

-   HBA からの割り込みを再度有効にします。

-   制御を返す

このルーチンが、マシンで他のデバイスの I/O 操作の使用を回避するためにできる限り迅速に実行する必要があることに注意してください。 その結果、 *HwScsiDisableInterruptsCallback*以上のコントロールを返す前に、HBA の割り込みを再度有効にする必要がありますしません。

 

 




