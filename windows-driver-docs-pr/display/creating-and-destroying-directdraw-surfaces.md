---
title: DirectDraw サーフェスの作成と破棄
description: DirectDraw サーフェスの作成と破棄
ms.assetid: d5557897-1810-448e-a2a8-aba96643b19c
keywords:
- 描画サーフェイス WDK DirectDraw、作成
- DirectDraw surface WDK Windows 2000 display, 作成
- WDK DirectDraw を作成し、作成します。
- 描画サーフェイス WDK DirectDraw、破棄
- DirectDraw surface WDK Windows 2000 display, 破棄
- WDK DirectDraw DirectDraw、破棄
- サーフェスの破棄 WDK DirectDraw
- Ddcanの場合
- Ddの/フェイス
- D3dCreateSurfaceEx
- DdDestroySurface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24780d6a9f8ab801160df5bd6e001558a8f22f96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839027"
---
# <a name="creating-and-destroying-directdraw-surfaces"></a>DirectDraw サーフェスの作成と破棄


## <span id="ddk_creating_and_destroying_directdraw_surfaces_gg"></span><span id="DDK_CREATING_AND_DESTROYING_DIRECTDRAW_SURFACES_GG"></span>


直接描画サーフェスは、4段階のプロセスで作成されます。 これらのステージは次のとおりです。

1.  [*Ddcan、* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85)) ランタイムは、ドライバーの*Ddcan/face*を呼び出して、ドライバーがこの種類、サイズ、および形式の表面を作成できるかどうかを確認します。 ドライバーは、アプリケーションに伝達されるエラーコードを返すことができます。

2.  [*Ddて*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))います。 このドライバーによって surface が作成され、サーフェイスのコンテンツにメモリが割り当てられる可能性があります。 複雑なサーフェスは、一度に1回だけ*作成すること*ができます。 そのため、ドライバーは、1回の呼び出しで多数のサーフェイスを作成する必要がある場合があります。

3.  メモリの割り当て。 DirectDraw ランタイムは、 [*dd記憶 Ur顔*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))呼び出しに応答して、ドライバーによって割り当てられていないすべてのサーフェイスにメモリを割り当てます。 このプロセスの詳細については、次のセクションで説明します。

4.  [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)。 この関数は、DirectX[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) token ストリームで後で使用するために、対象のサーフェイスにハンドルを関連付けます。 また、このドライバーは、この時点で DirectDraw によって保持されている表面構造の独自のコピーも作成します。 **D3dCreateSurfaceEx**の詳細については、DirectX Driver Development KIT (DDK) のドキュメントを参照してください。

DirectDraw ドライバーでは、 [**EngAllocUserMem**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocusermem)関数を呼び出すなどして、サーフェイスのユーザーモードのメモリを直接**割り当てることは**できません。   代わりに、ドライバーは、DirectDraw ランタイムがサーフェイスにユーザーモードのメモリを割り当てることができます。
ドライバーがメモリを直接割り当てた場合、その後、画面を作成したプロセス以外のプロセスによってビデオモードを変更するように要求すると、オペレーティングシステムのクラッシュやメモリリークが発生する可能性があります。 DirectDraw ランタイムによってユーザーモードのメモリが割り当てられるようにするには、ドライバーは、 [*Dd記憶 Urface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))関数からの DDHAL\_ASEASEALLOC\_usermem 値を返します。 詳細については、「 *ddの*参照」ページの「解説」を参照してください。

 

サーフェイスは、ドライバーの[*DdDestroySurface*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)エントリポイントへの1回の呼び出しによって破棄されます。これは、画面に割り当てられているか、サーフェスの作成中にメモリの割り当てに関係していた場合のみです。 DirectDraw ランタイムによってメモリが割り当てられ、ドライバーが関連していない場合、ランタイムは*DdDestroySurface*を呼び出しません。

サーフェイスは、作成されたモードが永続化されている限り保持されます。 モードが変更された場合、ドライバーの制御下にあるすべてのサーフェイスが破棄されます。 また、この方法ですべてのサーフェイスが破壊される可能性がある他のイベントもあります。 ドライバーが[*DdDestroySurface*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)呼び出しの原因を特定する必要はありません。

 

 





