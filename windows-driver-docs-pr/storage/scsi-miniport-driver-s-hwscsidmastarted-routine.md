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
ms.openlocfilehash: e2ce54683ae22235a5308c2828ecaeb4ce6b8c30
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606534"
---
# <a name="scsi-miniport-drivers-hwscsidmastarted-routine"></a>SCSI ミニポート ドライバーの HwScsiDmaStarted ルーチン

システム DMA コントローラーを使用する HBA のミニポートドライバーには、 [**HwScsiDmaStarted**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85))ルーチンが必要です。

データ転送操作の場合、このようなミニポートドライバーは[**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer)を呼び出す必要があります。これは、HBA ごとのデータのデバイス拡張機能へのポインターと、転送を要求する SRB に渡すと共に、データの転送元となるバッファーの論理アドレスの範囲を渡します。

**ScsiPortIoMapTransfer**に渡される論理アドレス範囲は、入力 SRB の**DataBuffer**と**datatransの長さ**、またはこの範囲の適切なサブセットに対してマップされた値であることに注意してください。 ほとんどの転送要求では、ミニポートドライバーライターは、入力 SRB に指定されたすべてのデータを1つの DMA 操作で転送できると想定できます。

特に、ミニポートドライバーでは、特定の SRB を満たすために複数の下位 DMA 転送操作を実行することが必要になる場合があります。これは、HBA がアプリケーション専用サポートを提供し、アプリケーションが大きな転送要求をミニポートドライバーに直接送信する場合のみです. それ以外の場合は、大規模な転送要求を一連の部分転送要求に分割し、それぞれが HBA の機能に合わせてサイズ変更されるように、ストレージクラスドライバーの役割を担います (「[ストレージクラスドライバー](introduction-to-storage-class-drivers.md)」を参照してください)。

**ScsiPortIoMapTransfer**は、システムの DMA コントローラーがシステムメモリと HBA の間でデータを転送する準備ができたときに、ミニポートドライバーの*HwScsiDmaStarted*ルーチンを呼び出します。 *HwScsiDmaStarted*は、転送操作用に HBA を設定する必要があります。

転送操作が完了したら、ミニポートドライバーは[**ScsiPortFlushDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportflushdma)を呼び出す必要があります。これは、SRB または呼び出し**ScsiPortIoMapTransfer**を使用して**ScsiPortNotification**を呼び出し、アプリケーションで提供されるバッファーのサブ範囲に対して、ユーザーモードアプリケーションのサポート専用の HBA である場合に、DMA コントローラーを再度設定します。

**ScsiPortFlushDma**は、DMA コントローラーにキャッシュされている残りのデータをフラッシュします。 ミニポートドライバーの*HwScsiDmaStarted*ルーチンがまだ呼び出されていない場合でも、 **ScsiPortFlushDma**を呼び出してシステム DMA 転送を取り消すことができます。

詳細については、「 [**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer) and [**ScsiPortFlushDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportflushdma) 」を参照してください。
