---
title: SCSI ミニポート ドライバーの HwScsiInitialize ルーチン
description: SCSI ミニポート ドライバーの HwScsiInitialize ルーチン
ms.assetid: 2a776c0a-1bac-4f8c-beab-fd53300f68c8
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiInitialize
- HwScsiInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ac72863ca0b2a7e5ff8a224c7c0781aec4031fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380595"
---
# <a name="scsi-miniport-drivers-hwscsiinitialize-routine"></a>SCSI ミニポート ドライバーの HwScsiInitialize ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiinitialize_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINITIALIZE_ROUTINE_KG"></span>


それぞれに、ミニポート ドライバーによって検出された HBA がサポートされているその[ *HwScsiInitialize* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))存在する場合に、HBA のレジスタとの初期状態を設定するルーチンが呼び出されます。

場合、 *HwScsiInitialize*ルーチンでは、HBA、ミニポート ドライバーの割り込みを有効に[ **HwScsiInterrupt** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))ルーチンは、デバイスの割り込みを処理するために呼び出されます初期化中に生成されます。

HBA の初期化とバスのリセットが発生した場合、 *HwScsiInitialize*ルーチンを呼び出す必要があります[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)で、 *NotificationType*値**ResetDetected**します。

 

 




