---
title: DirectDraw での浮動小数点演算の実行
description: DirectDraw での浮動小数点演算の実行
ms.assetid: 2ce638e8-2d32-4692-8093-adb413bfbe52
keywords:
- 浮動小数点演算 WDK DirectDraw
- WDK DirectDraw、浮動小数点演算の描画
- 浮動小数点演算、DirectDraw WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94fe18ca429ab07640306399adeab4ad35107466
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366400"
---
# <a name="performing-floating-point-operations-in-directdraw"></a>DirectDraw での浮動小数点演算の実行


## <span id="ddk_performing_floating_point_operations_in_directdraw_gg"></span><span id="DDK_PERFORMING_FLOATING_POINT_OPERATIONS_IN_DIRECTDRAW_GG"></span>


DirectDraw ドライバーのコールバック関数は、GDI が指定した呼び出しの間でのすべての浮動小数点演算を実行する必要があります[ **EngSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565010)と[ **EngRestoreFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565006)関数。 つまり、ドライバーのコールバック関数は浮動小数点演算を実行する前に、浮動小数点状態を保存する必要があります、浮動小数点演算が完了すると、浮動小数点状態を復元する必要があります。 浮動小数点演算の詳細については、次を参照してください。[グラフィックス ドライバー関数での浮動小数点操作](floating-point-operations-in-graphics-driver-functions.md)します。

 

 





