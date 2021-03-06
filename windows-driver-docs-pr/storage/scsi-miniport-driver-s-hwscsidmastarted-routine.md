---
title: SCSI ミニポート ドライバーの HwScsiDmaStarted ルーチン
description: SCSI ミニポート ドライバーの HwScsiDmaStarted ルーチン
ms.assetid: 697839f0-e912-42a5-abe0-f6bb946c86d8
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiDmaStarted
- HwScsiDmaStarted
- DMA コント ローラー WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c4cd44105e67674ca4a17c184b5dc98f6fe3571
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360179"
---
# <a name="scsi-miniport-drivers-hwscsidmastarted-routine"></a>SCSI ミニポート ドライバーの HwScsiDmaStarted ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsidmastarted_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDMASTARTED_ROUTINE_KG"></span>


システムの DMA コント ローラーを使用する HBA のミニポート ドライバーが必要、 [ **HwScsiDmaStarted** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85))ルーチン。

データ転送操作では、このようなミニポート ドライバーが呼び出す必要があります[ **ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportiomaptransfer)の HBA のデータをそのデバイスの拡張機能を転送を要求すると共に SRB のポインターを渡して、あるか、データを転送するのには、バッファーの論理アドレスの範囲。

渡される、論理アドレスの範囲を**ScsiPortIoMapTransfer**か、入力 SRB のマップされた値にする必要があります**DataBuffer**と**DataTransferLength**またはこの範囲の適切なサブセットです。 ほとんどの転送要求のミニポート ドライバーのライターは SRB の入力で指定されたすべてのデータを 1 つの DMA 操作で転送できることを想定できます。

具体的には、ミニポート ドライバーが HBA は、アプリケーション専用のサポートを提供します。 アプリケーション、ミニポート ドライバーに直接大きな転送要求を送信する場合にのみ、指定された SRB を満たすために、1 つ以上の従属する DMA 転送操作を実行する必要があります. それ以外の場合、部分的な転送要求のセットに大きな転送要求を分割する記憶域クラス ドライバーの役割です、それぞれの HBA の機能に合わせてサイズ (を参照してください[ストレージ クラス ドライバー](storage-class-drivers.md))。

**ScsiPortIoMapTransfer**呼び出し、ミニポート ドライバーの*HwScsiDmaStarted*ルーチン システム DMA コント ローラーがシステム メモリ、および HBA の間でデータを転送する準備ができたときです。 *HwScsiDmaStarted*転送操作の HBA を設定する必要があります。

転送操作が完了したら、ミニポート ドライバーで呼び出す必要があります[ **ScsiPortFlushDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportflushdma)を呼び出す前に**ScsiPortNotification** SRB やの呼び出し**ScsiPortIoMapTransfer** HBA は、ユーザー モード アプリケーションのサポートに専用の場合、アプリケーションによって提供されるバッファーにあるサブ範囲用にもう一度 DMA コント ローラーを設定します。

**ScsiPortFlushDma** DMA コント ローラーにキャッシュされている残りのデータをフラッシュします。 なお**ScsiPortFlushDma**も呼び出すことができる場合でも、システムの DMA の転送をキャンセルするミニポート ドライバーの*HwScsiDmaStarted*ルーチンが呼び出されていません。

参照してください[ **ScsiPortIoMapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportiomaptransfer)と[ **ScsiPortFlushDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportflushdma)詳細についてはします。

 

 




