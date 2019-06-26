---
title: PDEV の管理
description: PDEV の管理
ms.assetid: f7badbe8-b24f-438a-8937-95bb98de6310
keywords:
- PDEV WDK DirectDraw
- 描画の WDK DirectDraw PDEV
- DirectDraw WDK Windows 2000 の表示、PDEV
- PDEV WDK DirectDraw を無効になっています。
- PDEV WDK DirectDraw を有効になっています。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdc36ae04d725a4d369c71710319bc8b818bfa6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370140"
---
# <a name="managing-pdevs"></a>PDEV の管理


## <span id="ddk_managing_pdevs_gg"></span><span id="DDK_MANAGING_PDEVS_GG"></span>


**このトピックでは、以降 Windows 2000 のみに適用されます。**

ディスプレイ ドライバーを呼び出すスレッドの数は、デバイス上の既存の PDEVs の数に依存します。 各デバイスには、最大のアダプターの出力ごとの 1 つ有効になっている PDEV と無効になっている PDEVs の数に制限はありません。 PDEV が無効にするか、ドライバーを呼び出すことによって有効になっている[ **DrvAssertMode** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)関数。 ディスプレイ ドライバーは、有効と無効 PDEVs の混在を管理しているときに、オペレーティング システムは無効になっている PDEVs でドライバー関数を呼び出す複数のスレッドを同時に許可するときに、有効になっている PDEV ドライバー関数を呼び出しに 1 つのスレッドを許可します。 たとえば、 [ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt) PDEV によって破棄される別の無効化中に有効になっている PDEV で実行される可能性が[ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface). 1 つのディスプレイ ドライバー (たとえば、シナリオでは、複数モニター)、複数の有効な PDEVs を管理する場合でも、オペレーティング システムのみです 1 つのスレッドとそれらが有効な PDEVs のドライバーのコードを呼び出すことができます。

場合は、ディスプレイ ドライバーには、任意のグローバル リソースと PDEVs 間で共有されるハードウェアの状態を管理する必要があります、ディスプレイ ドライバーも必要な同期を処理する必要があります。 ディスプレイ ドライバーは、セッションごとに、独自のグローバル変数のセットがあるために、セッションの領域にマップされます。 そのため、ミュー テックスなどの同期オブジェクトを保持するのにディスプレイ ドライバーのグローバル変数を使用する必要がありますできません。 代わりに、グローバル空間にマップされているビデオのミニポート ドライバーのデバイスの拡張機能で、ミュー テックスを格納セッション領域ではなく。 ビデオのミニポート ドライバーのミュー テックスを初期化する[ *HwVidInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)関数。 次に、ディスプレイ ドライバーの[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)関数は、ビデオのミニポート ドライバーにカスタムの IOCTL を送信することによって、ミュー テックスへのポインターを取得できます。 別のセッションに属するドライバー スレッドを表示、ポインターのコピーを個別になりますが、同じミュー テックス オブジェクトを指すすべてのこれらのコピーは。

ディスプレイ ドライバーは、直接取得し、ディスプレイ ドライバーがこれらのタスクを実行するビデオのミニポート ドライバーに依存する必要がありますので、ミュー テックスを解放するカーネル ルーチンを呼び出すには許可されません。 ビデオのミニポート ドライバーを取得し、ミュー テックスを解放する関数を実装し、ディスプレイ ドライバーでした、ミュー テックス自体へのポインターを取得するために使用する同じカスタム IOCTL では、その関数へのポインターを取得します。

無効になっている PDEV ドライバー関数の次の制限数のみを呼び出すことができます。

-   [*DdMapMemory* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory) (のマッピング解除中のメモリのみ)

-   [**DrvDisableDirectDraw**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledirectdraw)

-   [**D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) (のシステム メモリの場合のみ)

-   [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [*DdDestroySurface*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)

-   [*DdLock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)

-   [*DdUnlock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)

-   [*DestroyD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552754(v=vs.85))

-   [*LockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))

-   [*UnlockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570106(v=vs.85))

-   [**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)

-   [**DrvDisablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)

-   [**DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)

-   [**DrvResetPDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)

 

 





