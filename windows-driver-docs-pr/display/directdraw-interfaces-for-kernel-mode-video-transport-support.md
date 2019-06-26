---
title: カーネル モードのビデオ トランスポート DirectDraw インターフェイス
description: カーネル モード ビデオ トランスポートのサポートのための DirectDraw インターフェイス
ms.assetid: 8012f6b0-3b55-438f-8146-4f62e6bafad3
keywords:
- カーネル モードのビデオ トランスポート WDK DirectDraw、インターフェイス
- DirectX VPE サポート WDK DirectDraw、カーネル モードのビデオ トランスポート
- 描画 VPEs WDK DirectDraw、カーネル モードのビデオ トランスポート
- DirectDraw VPEs WDK Windows 2000 の表示、カーネル モードのビデオ トランスポート
- 拡張機能のビデオ ポート WDK DirectDraw、カーネル モードのビデオ トランスポート
- VPEs WDK DirectDraw、カーネル モードのビデオ トランスポート
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 246454cd126e885e674340c9d8bb40bb0cd2e579
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384846"
---
# <a name="directdraw-interfaces-for-kernel-mode-video-transport-support"></a>カーネル モード ビデオ トランスポートのサポートのための DirectDraw インターフェイス

カーネル モードのビデオ トランスポートする必要がありますの追跡を使用して各画面および VPE オブジェクトごとに画面の情報。 この情報は、毎回更新する必要があります[ *DdUpdateOverlay* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_updateoverlay)または[ *DdVideoPortUpdate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_update)画面やハードウェアが呼び出されますビデオ ポート。 DirectDraw では、この情報をカーネル モードのビデオ トランスポートに送信する前に 2 つのドライバー関数のいずれかを呼び出します。[*DdSyncSurfaceData* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface)または[ *DdSyncVideoPortData*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport)します。 これらの関数入力するか、または構造体の情報の一部を変更して、4 つを使用するドライバーを許可する **dwDriverReserved * * * N*のメンバー、 [ **DD\_SYNCSURFACEDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_syncsurfacedata)または 3 つ **dwDriverReserved * * * N*のメンバー、 [ **DD\_SYNCVIDEOPORTDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_syncvideoportdata)独自の目的で構造体。 これらのドライバー関数は、正常に動作するカーネル モードのビデオ トランスポートのサポートに必要です。

ドライバーがこれらどのように使用方法の良い例 **dwDriverReserved * * * N*メンバーがどの物理オーバーレイ、オーバーレイの画面を示すフラグを設定するのには、ハードウェアは、1 つ以上の物理オーバーレイをサポートしている場合は使用できます。

 

 





