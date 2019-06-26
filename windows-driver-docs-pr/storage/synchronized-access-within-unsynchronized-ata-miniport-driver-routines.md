---
title: ATA のミニポート ドライバー ルーチン内の同期アクセス
description: 同期されていない ATA ミニポート ドライバー ルーチン内の同期アクセス
ms.assetid: ed047579-9f22-4725-a4b0-3c44b8db89ef
keywords:
- ATA ポート ドライバー WDK、同期
- WDK ATA ポート ドライバーの同期
- 同期されていない処理 WDK ATA ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b4835f91652cd490cd1a4f9291d1883fd0849e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368162"
---
# <a name="synchronized-access-within-ata-miniport-driver-routines"></a>ATA のミニポート ドライバー ルーチン内の同期アクセス


## <span id="ddk_synchronized_access_within_unsynchronized_ata_miniport_driver_rout"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_ATA_MINIPORT_DRIVER_ROUT"></span>


**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。


ATA のミニポート ドライバーがで I/O 要求の処理が同期されていないが場合にもその[ **IdeHwBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_buildio)ルーチンを同期する重要なシステムの構造体へのアクセスを呼び出して[ **AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportrequestsynchronizedroutine)します。 このルーチンに似ています、 [ **StorPortSynchronizeAccess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportsynchronizeaccess) Storport I/O モデルで提供されているルーチン。 Storport ミニポート ドライバーを管理する方法の詳細については、重要なデータ構造へのアクセスを同期を参照してください[同期されていないミニポート ドライバー ルーチン内のアクセスの同期](synchronized-access-within-unsynchronized-miniport-driver-routines.md)します。

ATA のミニポート ドライバーを呼び出すと**AtaPortRequestSynchronizedRoutine**、コールバック ルーチンへのポインターを指定する必要があります。 コールバック ルーチンは、割り込みハンドラーと同期する必要があります I/O 要求の一部を処理します。 パフォーマンスの向上のためには、コールバック ルーチンを実行することにかかる時間は、ドライバーを記述します。

 

 


