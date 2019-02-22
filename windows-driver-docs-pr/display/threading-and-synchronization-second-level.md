---
title: スレッド処理と第 2 レベルの同期
description: スレッド処理と第 2 レベルの同期
ms.assetid: 2b7c1eae-6527-469e-a2fa-74d2a1246bd3
keywords:
- WDK の表示をスレッドには、2 番目のレベル
- WDK 表示の同期、2 番目のレベル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bb006bc58e52674f1ad2d4f92ec0adbcddb153b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537072"
---
# <a name="threading-and-synchronization-second-level"></a>スレッド処理と第 2 レベルの同期


スレッドと同期の 2 番目のレベルが同じ[第 3 レベル](threading-and-synchronization-third-level.md), ビデオ メモリが CPU メモリをホストする削除されない点が異なります。 つまり、ディスプレイのミニポート ドライバー内で 1 つのスレッド (つまり、呼び出し元のスレッド) のみである Windows 表示 Driver Model (WDDM) の保証、グラフィックス ハードウェアがアイドル状態と、ダイレクト メモリ アクセス (DMA) バッファー現在によって処理されているなしドライバーまたは GPU スケジューラをパススルーします。 2 番目のレベルでは、ディスプレイのミニポート ドライバーには、次の呼び出しが行われます。

**注**  で一部の呼び出し、2 番目のレベルの下に作成するために、 **HardwareAccess**内でフラグを設定する必要があります、 **D3DDDI\_ESCAPEFLAGS**構造体メンバーである**DXGKARG\_エスケープ**します。 このフラグが設定されていない場合は、呼び出しは失敗します。

 

-   [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)

-   [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)

-   [*DxgkDdiDispatchIoRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_dispatch_io_request)

-   [*DxgkDdiEscape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)

-   [*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)

-   [*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)

-   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)

-   [*DxgkDdiRecommendMonitorModes*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendmonitormodes)

-   [*DxgkDdiSetPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpalette)

-   [*DxgkDdiSetTimingsFromVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)

-   [*DxgkDdiSetVidPnSourceAddress*](https://msdn.microsoft.com/library/windows/hardware/ff560767)

-   [*DxgkDdiSetVidPnSourceVisibility*](https://msdn.microsoft.com/library/windows/hardware/ff560771)

-   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)

 

 





