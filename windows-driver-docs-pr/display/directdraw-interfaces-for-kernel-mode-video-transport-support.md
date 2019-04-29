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
ms.openlocfilehash: 27f058bd394289246e0cd937711cbdf325b1ed2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392056"
---
# <a name="directdraw-interfaces-for-kernel-mode-video-transport-support"></a>カーネル モード ビデオ トランスポートのサポートのための DirectDraw インターフェイス

カーネル モードのビデオ トランスポートする必要がありますの追跡を使用して各画面および VPE オブジェクトごとに画面の情報。 この情報は、毎回更新する必要があります[ *DdUpdateOverlay* ](https://msdn.microsoft.com/library/windows/hardware/ff550369)または[ *DdVideoPortUpdate* ](https://msdn.microsoft.com/library/windows/hardware/ff550450)画面やハードウェアが呼び出されますビデオ ポート。 DirectDraw では、この情報をカーネル モードのビデオ トランスポートに送信する前に 2 つのドライバー関数のいずれかを呼び出します。[*DdSyncSurfaceData* ](https://msdn.microsoft.com/library/windows/hardware/ff550345)または[ *DdSyncVideoPortData*](https://msdn.microsoft.com/library/windows/hardware/ff550350)します。 これらの関数入力するか、または構造体の情報の一部を変更して、4 つを使用するドライバーを許可する **dwDriverReserved * * * N*のメンバー、 [ **DD\_SYNCSURFACEDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551739)または 3 つ **dwDriverReserved * * * N*のメンバー、 [ **DD\_SYNCVIDEOPORTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551740)独自の目的で構造体。 これらのドライバー関数は、正常に動作するカーネル モードのビデオ トランスポートのサポートに必要です。

ドライバーがこれらどのように使用方法の良い例 **dwDriverReserved * * * N*メンバーがどの物理オーバーレイ、オーバーレイの画面を示すフラグを設定するのには、ハードウェアは、1 つ以上の物理オーバーレイをサポートしている場合は使用できます。

 

 





