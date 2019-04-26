---
title: DirectDraw サーフェスの作成と復元
description: DirectDraw サーフェスの作成と復元
ms.assetid: 74203932-8a30-44ea-8d0d-45265dd2e74a
keywords:
- 描画サーフェスの WDK DirectDraw、失われる
- DirectDraw サーフェス WDK Windows 2000 を表示するが失われる
- WDK DirectDraw、サーフェスが失われる
- 描画サーフェイス WDK DirectDraw、復元します。
- DirectDraw サーフェス WDK Windows 2000 の表示、復元します。
- WDK DirectDraw、サーフェスを復元します。
- サーフェス WDK DirectDraw を復元します。
- 失われたサーフェス WDK DirectDraw
- 中断されたサーフェス WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb0483064a05bc44f18cd250fd3fea3a0fd6e34c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347502"
---
# <a name="losing-and-restoring-directdraw-surfaces"></a>DirectDraw サーフェスの作成と復元


## <span id="ddk_losing_and_restoring_directdraw_surfaces_gg"></span><span id="DDK_LOSING_AND_RESTORING_DIRECTDRAW_SURFACES_GG"></span>


画面のオブジェクトの有効期間は、ドライバーの表面のオブジェクトの場合より、ランタイムの表面のオブジェクトの長くなります。 一部の状況において最も顕著なモードの変更、サーフェスが*失わ*します。 これは、ドライバーの表面のオブジェクトが破棄されることを意味と[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)を呼び出すと、ランタイムの表面のオブジェクトが中断状態に格納されます。 ランタイム オブジェクトは、後で、*復元*に対応する、 [ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)ドライバー レベルで呼び出します。

通常、ドライバーは、この中間の失われた状態の注意すべきはありません。 ただし、場合によってはこのプロセスの理解がドライバー開発者を支援する場所があります。

ドライバーの作成者は、1 つのアトミックな呼び出しで複雑な表面の復元を処理することができます。 画面の復元時に、DirectDraw ランタイムは、ドライバーを調べて[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)エントリ ポイント。 このエントリ ポイントが定義されているかどうかは、DirectDraw ランタイムに 1 回の呼び出しですべての複雑なサーフェイスの復元[ *DdCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549263)します。 ドライバーおそらくできなく元の作成と、画面の復元による作成を区別します。

 

 





