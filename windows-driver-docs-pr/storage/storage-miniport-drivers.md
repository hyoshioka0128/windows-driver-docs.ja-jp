---
title: ストレージ ミニポート ドライバー
description: ストレージ ミニポート ドライバー
ms.assetid: 374d8370-02a9-43ab-ab47-27fa9f4051ea
keywords:
- ストレージ ミニポート ドライバー WDK
- ミニポート ドライバー WDK ストレージ
- ストレージ ドライバー WDK、ミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5f9c1e02583436ac3af9d0feaca0a121455c93c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553439"
---
# <a name="storage-miniport-drivers"></a>ストレージ ミニポート ドライバー


## <span id="ddk_storage_miniport_drivers_kg"></span><span id="DDK_STORAGE_MINIPORT_DRIVERS_KG"></span>


このセクションには、次のトピックが含まれています。

[SCSI ミニポート ドライバー](scsi-miniport-drivers.md)

[Storport ミニポート ドライバー](storport-miniport-drivers.md)

[IDE コント ローラーのミニドライバー](ide-controller-minidrivers.md)

[ATA のミニポート ドライバー](ata-miniport-drivers.md)

ストレージ ミニポート ドライバーのベスト プラクティスは、ポートのドライバー サポート ライブラリを提供するルーチン以外のオペレーティング システムのルーチンを呼び出すことを回避するためにです。 たとえば、記憶域ミニポート ドライバー呼び出さないでください[ **KeQuerySystemTime**](https://msdn.microsoft.com/library/windows/hardware/ff553068)します。 代わりに、ミニポート ドライバーはのようなルーチンを呼び出す必要があります[ **ScsiPortQuerySystemTime** ](https://msdn.microsoft.com/library/windows/hardware/ff564708)または[ **StorPortQuerySystemTime**](https://msdn.microsoft.com/library/windows/hardware/ff567465)します。 ストレージ ミニポート ドライバーは呼び出さないでください[ **MmGetPhysicalAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554547)します。 代わりに、ミニポート ドライバーはのようなルーチンを呼び出す必要があります[ **ScsiPortGetPhysicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff564636)と[ **StorPortGetPhysicalAddress**](https://msdn.microsoft.com/library/windows/hardware/ff567095)します。

使用しない[ハードウェア アブストラクション レイヤー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff546644)ミニポート ドライバーでします。

次の一覧では、記憶域ミニポート ドライバーの種類ごとに使用するポートのドライバー サポート ライブラリを示します。

-   SCSI ポート ミニポート ドライバー:[ライブラリ ルーチンの SCSI ポート](required-and-optional-scsi-miniport-driver-routines.md)

-   Storport ミニポート ドライバー:[Storport ドライバー サポート ルーチン](storport-driver-support-routines.md)

-   IDE のミニポート ドライバー:[PciIdeX ライブラリ ルーチン](ide-controller-minidrivers.md)

-   ATA のポートのミニポート ドライバー:[ATA ポート ライブラリ ルーチン](ata-miniport-drivers.md)

 

 




