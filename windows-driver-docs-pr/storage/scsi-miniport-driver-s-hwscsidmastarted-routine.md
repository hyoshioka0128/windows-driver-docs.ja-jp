---
title: SCSI ミニポート ドライバーの HwScsiDmaStarted ルーチン
description: SCSI ミニポート ドライバーの HwScsiDmaStarted ルーチン
ms.assetid: 697839f0-e912-42a5-abe0-f6bb946c86d8
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiDmaStarted
- HwScsiDmaStarted
- DMA コントローラー WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f79b6f7b24c3a565e6038a375746de3b72abb1e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842676"
---
# <a name="scsi-miniport-drivers-hwscsidmastarted-routine"></a>SCSI ミニポート ドライバーの HwScsiDmaStarted ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsidmastarted_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDMASTARTED_ROUTINE_KG"></span>


システム DMA コントローラーを使用する HBA のミニポートドライバーには、 [**HwScsiDmaStarted**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85))ルーチンが必要です。

データ転送操作の場合、このようなミニポートドライバーは[**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer)を呼び出す必要があります。そのためには、HBA データごとのデバイス拡張機能へのポインターと、転送を要求している SRB に渡す必要があります。または、データが転送されます。

**ScsiPortIoMapTransfer**に渡される論理アドレス範囲は、入力 SRB の**DataBuffer**と**datatransの長さ**、またはこの範囲の適切なサブセットに対してマップされた値であることに注意してください。 ほとんどの転送要求では、ミニポートドライバーライターは、入力 SRB に指定されたすべてのデータを1つの DMA 操作で転送できると想定できます。

特に、ミニポートドライバーでは、特定の SRB を満たすために複数の下位 DMA 転送操作を実行することが必要になる場合があります。これは、HBA がアプリケーション専用サポートを提供し、アプリケーションが大きな転送要求をミニポートドライバーに直接送信する場合のみです. それ以外の場合は、大規模な転送要求を一連の部分転送要求に分割し、それぞれが HBA の機能に合わせてサイズ変更されるように、ストレージクラスドライバーの役割を担います (「[ストレージクラスドライバー](storage-class-drivers.md)」を参照してください)。

**ScsiPortIoMapTransfer**は、システムの DMA コントローラーがシステムメモリと HBA の間でデータを転送する準備ができたときに、ミニポートドライバーの*HwScsiDmaStarted*ルーチンを呼び出します。 *HwScsiDmaStarted*は、転送操作用に HBA を設定する必要があります。

転送操作が完了したら、ミニポートドライバーは[**ScsiPortFlushDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportflushdma)を呼び出す必要があります。その前に、SRB または**ScsiPortIoMapTransfer**を呼び出して**ScsiPortNotification**を呼び出し、ユーザーモードアプリケーションのサポート専用の HBA の場合は、アプリケーションによって提供されるバッファー。

**ScsiPortFlushDma**は、DMA コントローラーにキャッシュされている残りのデータをフラッシュします。 ミニポートドライバーの*HwScsiDmaStarted*ルーチンがまだ呼び出されていない場合でも、 **ScsiPortFlushDma**を呼び出してシステム DMA 転送を取り消すことができます。

詳細については、「 [**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer) and [**ScsiPortFlushDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportflushdma) 」を参照してください。

 

 




