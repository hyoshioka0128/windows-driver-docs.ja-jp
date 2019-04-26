---
title: DirectDraw サーフェスの作成と破棄
description: DirectDraw サーフェスの作成と破棄
ms.assetid: d5557897-1810-448e-a2a8-aba96643b19c
keywords:
- 描画サーフェイス WDK DirectDraw、作成します。
- DirectDraw サーフェス WDK Windows 2000 の表示、作成します。
- WDK DirectDraw、サーフェスを作成します。
- 描画サーフェイス WDK DirectDraw を破棄し、
- 破棄、DirectDraw サーフェス WDK Windows 2000 を表示します。
- WDK DirectDraw、サーフェスを破棄します。
- サーフェス WDK DirectDraw を破棄します。
- DdCanCreateSurface
- DdCreateSurface
- D3dCreateSurfaceEx
- DdDestroySurface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d26ee923972cf76b2de93340d4cc88b6a51fdc46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346915"
---
# <a name="creating-and-destroying-directdraw-surfaces"></a>DirectDraw サーフェスの作成と破棄


## <span id="ddk_creating_and_destroying_directdraw_surfaces_gg"></span><span id="DDK_CREATING_AND_DESTROYING_DIRECTDRAW_SURFACES_GG"></span>


直接描画サーフェスは、4 段階のプロセスで作成されます。 これらの各段階は次のとおりです。

1.  [*DdCanCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549213)します。 ランタイムが呼び出す、ドライバーの*DdCanCreateSurface*にドライバーがこの種類、サイズ、および形式のサーフェスの作成を許可するかどうかを参照してください。 ドライバーは、アプリケーションに反映されるエラー コードを返すことができます。

2.  [*DdCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549263)します。 ドライバーは、可能性のあるメモリを割り当て、画面の内容の画面を作成します。 1 回の呼び出しで複雑なサーフェスをすべて一度に作成できる*DdCreateSurface*します。 そのため、ドライバーは、1 回の呼び出しで多数のサーフェスを作成する必要があります。

3.  メモリの割り当て。 DirectDraw ランタイムのサーフェイスへの応答中にドライバーによって割り当てられていないメモリを割り当てます、 [ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)呼び出します。 このプロセスは、次のセクションで詳しく説明します。

4.  [**D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)します。 この関数は、DirectX の後で使用できる対象の画面をハンドルを関連付けます[**D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)トークン ストリーム。 ドライバーには、この時点で、DirectDraw によって管理される表面の構造体の独自のコピーも作成します。 詳細については**D3dCreateSurfaceEx**、DirectX ドライバー開発キット (DDK) ドキュメントを参照してください。

**注**   A DirectDraw ドライバー サーフェスのユーザー モードのメモリを割り当てる必要があります直接ではなく (など、呼び出すことによって、 [ **EngAllocUserMem** ](https://msdn.microsoft.com/library/windows/hardware/ff564178)関数)。 代わりに、ドライバー、DirectDraw ランタイムのサーフェスのユーザー モードのメモリを割り当てることができます。
ドライバーは、直接メモリを割り当てて、以外のオペレーティング システムのクラッシュまたはメモリが発生する可能性があります、画面を作成したプロセスによってビデオ モードを変更する後続の要求がリークします。 ユーザー モードのメモリを割り当て、DirectDraw ランタイムには、ドライバーは、DDHAL を返す必要があります\_PLEASEALLOC\_USERMEM 値からその[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)関数。 詳細についてで「解説」を参照してください。、 *DdCreateSurface*リファレンス ページです。

 

サーフェスは、ドライバーの単一の呼び出しによって破棄される[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)ドライバーが割り当てられているかが画面の作成時に、画面のメモリの割り当てに関連する場合にのみ、エントリ ポイント。 ランタイムは呼び出しません DirectDraw ランタイムがメモリを割り当て、ドライバーが含まれていない場合は、 *DdDestroySurface*します。

サーフェスは保持と、作成モードが解決しない限りのみです。 モードの変更では、ドライバーの管理下にあるすべてのサーフェイスが破棄、ドライバーがに関する限りされます。 この方法で破棄するすべてのサーフェスを引き起こす可能性のあるその他のイベントもあります。 ドライバーの原因を特定するための必要はありません、 [ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)呼び出します。

 

 





