---
title: SCSI ミニポート初期化の順序への依存禁止
description: SCSI ミニポート初期化の順序への依存禁止
ms.assetid: 762fa062-4eaa-40f2-acdb-99fc6cafe680
keywords:
- SCSI ミニポートドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- WDK SCSI のプラグアンドプレイ
- SCSI ミニポートドライバーの変換
- SCSI ミニポートドライバーの初期化
- SCSI ミニポートドライバー WDK ストレージ、初期化
- 順序依存コード WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47c08b3b939a29772ef8c686e9a388810a19ec3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845173"
---
# <a name="do-not-depend-on-order-of-scsi-miniport-initialization"></a>SCSI ミニポート初期化の順序への依存禁止


## <span id="ddk_do_not_depend_on_order_of_scsi_miniport_initialization_kg"></span><span id="DDK_DO_NOT_DEPEND_ON_ORDER_OF_SCSI_MINIPORT_INITIALIZATION_KG"></span>


一部のミニポートドライバーは、PCI、EISA、ISA など、いくつかの異なるシステムバス上の Hba をサポートしています。 Microsoft Windows NT 4.0 では、このようなミニポートドライバーの*HwScsiFindAdapter*ルーチンは、ミニポートドライバーが[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)を呼び出した順序で呼び出されました。 場合によっては、この方法を使用して、ある種類のバスでカードの場所を追跡することによって、ミニポートドライバーが別のポートを検出しないようにすることができます。

たとえば、ISA バスで Twiddle PCI SCSI HBA にもアクセスできるとします。 Windows NT 4.0 では、Twiddle ミニポートドライバーは、初期化のために呼び出された PCI Hba と、それが登場した ISA バスの場所を追跡します。 ミニポートドライバーは、ISA バスのスキャン中にこの情報を使用して、スキップする i/o 範囲を特定できます。

Windows 2000 以降では、この手法は信頼できなくなりました。 プラグアンドプレイは初期化の順序が予測できないため、Twiddle ミニポートドライバーを呼び出して、その PCI カードを初期化する前に ISA カードをスキャンするのが簡単になります。 ミニポートドライバーによって各 PCI HBA が2回検出されるため、システムがクラッシュする可能性があります。

この場合、カードの実際のバスインターフェイスを特定するために使用できるコマンドが Twiddle HBA にあると、ISA バススキャンによって検出された各カードに対してクエリを実行できます。 カードが ISA カードではなく PCI カードの場合、Twiddle ミニポートドライバーは、そのカードを取得するためにプラグアンドプレイ発行されるまで、そのカードをそのままにします。

ミニポートドライバーの順序に依存するコードを削除できない場合は、Windows 2000 以降のプラットフォームでレガシドライバーとして実行する必要があります。

 

 




