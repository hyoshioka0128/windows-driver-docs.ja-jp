---
title: ATA ポート ドライバーの概要
description: ATA ポート ドライバーの概要
ms.assetid: c7b9d794-a8cb-4bdd-bb93-bff473ea26a7
keywords:
- ストレージポートドライバー WDK、ATA ポートドライバー
- ATA ポートドライバー WDK
- Ata ポートドライバー WDK、ATA ポートドライバーについて
- IDE コントローラー WDK ATA ポートドライバー
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9e57e9325aba73063b3a18ee99afe19e6b6c2943
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606496"
---
# <a name="ata-port-driver-overview"></a>ATA ポート ドライバーの概要

> [!NOTE]
> ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](storport-driver-overview.md)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。

[SCSI ポートドライバー](scsi-port-driver-overview.md)および[Storport ドライバー](storport-driver-overview.md)に加えて、windows Vista 以降のバージョンの windows オペレーティングシステムには、ATA ポートドライバー (*Ataport*) が用意されています。これは、特に IDE コントローラーでの使用に適したストレージポートドライバーです。

ATA ポートドライバーとその他のシステム提供のストレージポートドライバーの最も重要な違いは、ATA ポートドライバーが他のドライバーとの通信に使用するプロトコルです。 システムが提供するその他のすべての記憶域ポートドライバーは、SCSI 要求ブロック (SRBs) を使用して、記憶域クラスドライバーやミニポートドライバーなどの上位レベルのドライバーとの両方を通信します。 ATA ポートドライバーは、SRBs を使用して、上位レベルのドライバーとのみ通信します。 ATA ポートは、そのミニポートドライバーと通信するために、 [IDE_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/ns-irb-_ide_request_block)構造によって定義される IDE 要求ブロック (IRB) と呼ばれるパケットを使用します。 IRBs は、ATA デバイスの特性に SRBs するよりも優れた設計になっています。

ATA ポートドライバーとその他のシステム提供の記憶装置ドライバーのもう1つの違いは、ata ポートドライバーが、SCSI 標準で定義されている特定の要件から ATA ミニポートドライバーをシールドすることです。 たとえば、ata ポートドライバーは ata コマンドを使用して ata ミニポートドライバーから同等の SCSI sense データを収集し、そのデータを SCSI sense データ形式に準拠するように変換して、そのデータを SCSI sense データであるかのように上位レベルのドライバーに渡します。 そのため、ATA ミニポートドライバーは、SCSI sense データ用の上位レベルのドライバーからの要求に直接応答する必要はありません。

ATA ミニポートドライバーのインターフェイスは、SCSI ポートドライバーのインターフェイスによく似ています。 したがって、SCSI ミニポートドライバーを既に作成してある場合は、ATA ミニポートドライバーの記述方法を簡単に習得できます。 Serial ATA (SATA) などの現在の ATA/ATAPI テクノロジのドライバーでは、より高いパフォーマンスの Storport ミニポートインターフェイスを使用する必要があります。

ATA ポートドライバーと共に、オペレーティングシステムは既定の ATA ミニポートドライバーと既定のコントローラーミニドライバーを提供します。 システムが提供する既定のドライバーは、ほとんどのコントローラーハードウェアで動作するため、可能な限り既定のミニドライバーを使用することを強くお勧めします。
