---
title: ATA ミニポートドライバールーチン内の同期されたアクセス
description: 同期されていない ATA ミニポート ドライバー ルーチン内の同期アクセス
ms.assetid: ed047579-9f22-4725-a4b0-3c44b8db89ef
keywords:
- ATA ポートドライバー WDK、同期
- 同期 WDK ATA ポートドライバー
- 非同期処理の WDK ATA ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de2bc7d3b818d10689c1f89852ac6b33fb4cd2db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842831"
---
# <a name="synchronized-access-within-ata-miniport-driver-routines"></a>ATA ミニポートドライバールーチン内の同期されたアクセス


## <span id="ddk_synchronized_access_within_unsynchronized_ata_miniport_driver_rout"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_ATA_MINIPORT_DRIVER_ROUT"></span>


**メモ**ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。


ATA ミニポートドライバーで[**IdeHwBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_buildio)ルーチン内の i/o 要求の非同期処理が行われている場合でも、 [**AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportrequestsynchronizedroutine)を呼び出すことによって、重要なシステム構造へのアクセスを同期できます。 このルーチンは、Storport i/o モデルに用意されている[**StorPortSynchronizeAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportsynchronizeaccess)ルーチンに似ています。 Storport ミニポートドライバーが重要なデータ構造の同期アクセスを管理する方法の詳細については、「同期されたアクセスを使用した[ミニポートドライバールーチン内のアクセス](synchronized-access-within-unsynchronized-miniport-driver-routines.md)」を参照してください。

ATA ミニポートドライバーは**AtaPortRequestSynchronizedRoutine**を呼び出すときに、コールバックルーチンへのポインターを提供する必要があります。 コールバックルーチンは、割り込みハンドラーと同期する必要がある i/o 要求の一部を処理します。 パフォーマンスを向上させるには、コールバックルーチンを実行するためにできるだけ短い時間だけ使用するようにドライバーを記述します。

 

 


