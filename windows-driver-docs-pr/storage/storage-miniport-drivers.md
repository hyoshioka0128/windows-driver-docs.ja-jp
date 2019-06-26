---
title: 記憶域ミニポート ドライバー
description: 記憶域ミニポート ドライバー
ms.assetid: 374d8370-02a9-43ab-ab47-27fa9f4051ea
keywords:
- ストレージ ミニポート ドライバー WDK
- ミニポート ドライバー WDK ストレージ
- ストレージ ドライバー WDK、ミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990d1ca49e6082613eb196b9db64d986bda92072
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368200"
---
# <a name="storage-miniport-drivers"></a>記憶域ミニポート ドライバー


## <span id="ddk_storage_miniport_drivers_kg"></span><span id="DDK_STORAGE_MINIPORT_DRIVERS_KG"></span>


このセクションでは、次のトピックについて説明します。

[SCSI ミニポート ドライバー](scsi-miniport-drivers.md)

[Storport ミニポート ドライバー](storport-miniport-drivers.md)

[IDE コント ローラーのミニドライバー](ide-controller-minidrivers.md)

[ATA のミニポート ドライバー](ata-miniport-drivers.md)

ストレージ ミニポート ドライバーのベスト プラクティスは、ポートのドライバー サポート ライブラリを提供するルーチン以外のオペレーティング システムのルーチンを呼び出すことを回避するためにです。 たとえば、記憶域ミニポート ドライバー呼び出さないでください[ **KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerysystemtime)します。 代わりに、ミニポート ドライバーはのようなルーチンを呼び出す必要があります[ **ScsiPortQuerySystemTime** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportquerysystemtime)または[ **StorPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportquerysystemtime)します。 ストレージ ミニポート ドライバーは呼び出さないでください[ **MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmgetphysicaladdress)します。 代わりに、ミニポート ドライバーはのようなルーチンを呼び出す必要があります[ **ScsiPortGetPhysicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetphysicaladdress)と[ **StorPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetphysicaladdress)します。

使用しない[ハードウェア アブストラクション レイヤー ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))ミニポート ドライバーでします。

次の一覧では、記憶域ミニポート ドライバーの種類ごとに使用するポートのドライバー サポート ライブラリを示します。

-   SCSI ポート ミニポート ドライバー:[ライブラリ ルーチンの SCSI ポート](required-and-optional-scsi-miniport-driver-routines.md)

-   Storport ミニポート ドライバー:[Storport ドライバー サポート ルーチン](storport-driver-support-routines.md)

-   IDE のミニポート ドライバー:[PciIdeX ライブラリ ルーチン](ide-controller-minidrivers.md)

-   ATA のポートのミニポート ドライバー:[ATA ポート ライブラリ ルーチン](ata-miniport-drivers.md)

 

 




