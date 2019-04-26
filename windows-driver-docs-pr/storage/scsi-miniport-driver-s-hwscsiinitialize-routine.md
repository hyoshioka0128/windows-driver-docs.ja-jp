---
title: SCSI ミニポート ドライバーの HwScsiInitialize ルーチン
description: SCSI ミニポート ドライバーの HwScsiInitialize ルーチン
ms.assetid: 2a776c0a-1bac-4f8c-beab-fd53300f68c8
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiInitialize
- HwScsiInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb53bff091d90541f1c67f5b13f51b900920f476
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339858"
---
# <a name="scsi-miniport-drivers-hwscsiinitialize-routine"></a>SCSI ミニポート ドライバーの HwScsiInitialize ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsiinitialize_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINITIALIZE_ROUTINE_KG"></span>


それぞれに、ミニポート ドライバーによって検出された HBA がサポートされているその[ *HwScsiInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff557302)存在する場合に、HBA のレジスタとの初期状態を設定するルーチンが呼び出されます。

場合、 *HwScsiInitialize*ルーチンでは、HBA、ミニポート ドライバーの割り込みを有効に[ **HwScsiInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff557312)ルーチンは、デバイスの割り込みを処理するために呼び出されます初期化中に生成されます。

HBA の初期化とバスのリセットが発生した場合、 *HwScsiInitialize*ルーチンを呼び出す必要があります[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)で、 *NotificationType*値**ResetDetected**します。

 

 




