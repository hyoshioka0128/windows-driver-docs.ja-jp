---
title: SCSI ミニポート ドライバーの HwScsiInitialize ルーチン
description: SCSI ミニポート ドライバーの HwScsiInitialize ルーチン
ms.assetid: 2a776c0a-1bac-4f8c-beab-fd53300f68c8
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiInitialize
- HwScsiInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 838a9c6c57205d1bb8da201bd14ec56aa4bb4c27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842668"
---
# <a name="scsi-miniport-drivers-hwscsiinitialize-routine"></a>SCSI ミニポート ドライバーの HwScsiInitialize ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiinitialize_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINITIALIZE_ROUTINE_KG"></span>


ミニポートドライバーによって検出されたサポートされる HBA ごとに、その[*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))ルーチンが呼び出され、hba のレジスタと初期状態 (存在する場合) が設定されます。

*HwScsiInitialize*ルーチンで HBA の割り込みが有効になっている場合は、初期化中にデバイスが生成するすべての割り込みを処理するために、ミニポートドライバーの[**HwScsiInterrupt**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))ルーチンが呼び出されます。

HBA を初期化するとバスがリセットされる場合、 *HwScsiInitialize*ルーチンは*NotificationType*値**Resetdetected 検出さ**れた[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)を呼び出す必要があります。

 

 




