---
title: 記憶域ミニポート ドライバー
description: 記憶域ミニポート ドライバー
ms.assetid: 374d8370-02a9-43ab-ab47-27fa9f4051ea
keywords:
- 記憶域ミニポートドライバー WDK
- ミニポートドライバー WDK ストレージ
- 記憶域ドライバー WDK、ミニポートドライバー
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: bd8ec22ccf78f1ae947dfcb0fb98fa81f64e7ae8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844465"
---
# <a name="storage-miniport-drivers"></a>記憶域ミニポート ドライバー

このセクションでは、次のトピックについて説明します。

[SCSI ミニポートドライバー](scsi-miniport-drivers.md)

[Storport ミニポートドライバー](storport-miniport-drivers.md)

[IDE コントローラーミニドライバー](ide-controller-minidrivers.md)

[ATA ミニポートドライバー](ata-miniport-drivers.md)

記憶域ミニポートドライバーのベストプラクティスは、適切なポートドライバーサポートによって提供されるサポートルーチン以外のオペレーティングシステムルーチンを呼び出さないようにすることです。 たとえば、ストレージミニポートドライバーは[**Kequerysystemtime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)を呼び出すことはできません。 代わりに、ミニポートドライバーは、 [**ScsiPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportquerysystemtime)や[**Storportquerysystemtime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportquerysystemtime)などのルーチンを呼び出す必要があります。 記憶域ミニポートドライバーは、 [**MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress)を呼び出すことはできません。 代わりに、ミニポートドライバーは、 [**ScsiPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress)や[**StorPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetphysicaladdress)などのルーチンを呼び出す必要があります。

ミニポートドライバーでは、[ハードウェアアブストラクションレイヤールーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))を使用しないでください。

次の一覧は、各種類の記憶域ミニポートドライバーで使用する必要がある、システムで指定されたポートドライバーのサポートライブラリを示しています。

| ミニポートドライバー | ポートドライバー |
| --------------- | ----------- |
| Storport ミニポートドライバー  | Windows Server 2003 およびそれ以降のバージョンのオペレーティングシステムで使用可能な[Storport ドライバー](storport-driver-overview.md) (*storport*) (推奨) |
| SCSI ポートミニポートドライバー | [SCSI ポートドライバー](scsi-port-driver-overview.md) (*Scsiport*) |
| ATA ポートミニポートドライバー  | Windows Vista 以降のバージョンのオペレーティングシステムで使用可能な[ATA ポートドライバー](ata-port-driver-overview.md) (*Ataport*) |
| IDE ミニポートドライバー       | 「 [IDE ポートドライバー](ide-port-driver.md) 」を参照してください。 |
