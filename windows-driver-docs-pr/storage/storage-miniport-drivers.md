---
title: Storage ミニポートドライバーの概要
description: 記憶域ミニポート ドライバー
ms.assetid: 374d8370-02a9-43ab-ab47-27fa9f4051ea
keywords:
- 記憶域ミニポートドライバー WDK
- ミニポートドライバー WDK ストレージ
- 記憶域ドライバー WDK、ミニポートドライバー
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5814bf08d138040ae5ea7ee7629dcde825be058d
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606552"
---
# <a name="introduction-to-storage-miniport-drivers"></a>Storage ミニポートドライバーの概要

ベンダーが提供する記憶域ミニポートドライバーは、システムによって提供される記憶域ポートドライバーと連携して、Windows 上のベンダーの記憶装置をサポートします。 これらのモジュール間の通信は次のように行われます。

- ミニポートは、一連のストレージポートドライバーが提供するサポートルーチンを呼び出します。

- ミニポートは、ストレージポートドライバーが呼び出すルーチンの標準セットを実装します。これは必須であり、省略可能なものもあります。

SCSI ポートドライバー、Storport ドライバー、および ATA ポートドライバーによって呼び出されるミニポートドライバールーチンは、互いによく似ています。

次の表に、記憶域ミニポートドライバーの種類と、それに関連付けられているシステム指定のポートドライバーサポートライブラリを示します。

| ミニポートドライバー | ポートドライバー |
| --------------- | ----------- |
| [Storport ミニポートドライバー](storport-miniport-drivers.md) | Windows Server 2003 およびそれ以降のバージョンのオペレーティングシステムで使用可能な[Storport ドライバー](storport-driver-overview.md) (*storport*) (推奨) |
| [SCSI ミニポートドライバー](scsi-miniport-drivers.md) | [SCSI ポートドライバー](scsi-port-driver-overview.md) (*Scsiport*) |
| [ATA ミニポートドライバー](ata-miniport-drivers.md) | Windows Vista 以降のバージョンのオペレーティングシステムで使用可能な[ATA ポートドライバー](ata-port-driver-overview.md) (*Ataport*) |
| [IDE コントローラーミニドライバー](requirements-for-vendor-supplied-ide-controller-minidrivers.md) | 「 [IDE ポートドライバー](ide-port-driver.md) 」を参照してください。 |

記憶域ミニポートドライバーのベストプラクティスは、適切なポートドライバーサポートによって提供されるサポートルーチン以外のオペレーティングシステムルーチンを呼び出さないようにすることです。 たとえば、ストレージミニポートドライバーは[**Kequerysystemtime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)を呼び出すことはできません。 代わりに、ミニポートドライバーは、 [**ScsiPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportquerysystemtime)や[**Storportquerysystemtime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportquerysystemtime)などのルーチンを呼び出す必要があります。 記憶域ミニポートドライバーは、 [**MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress)を呼び出すことはできません。 代わりに、ミニポートドライバーは、 [**ScsiPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress)や[**StorPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetphysicaladdress)などのルーチンを呼び出す必要があります。

ミニポートドライバーでは、[ハードウェアアブストラクションレイヤールーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))を使用しないでください。
