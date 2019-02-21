---
title: 色ポインターの描画
description: 色ポインターの描画
ms.assetid: f2791ccc-3d9e-46f0-bc70-051ac298c1ee
keywords:
- 描画ポインター WDK Windows 2000 を表示します。
- ディスプレイ ドライバー WDK Windows 2000 では、ポインター
- Windows 2000 の WDK のポインターを表示します。
- Windows 2000 の WDK のポインターの色の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49424ca9fd9b40b375da98debfb79bdb3bfb98a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528388"
---
# <a name="drawing-color-pointers"></a>色ポインターの描画


## <span id="ddk_drawing_color_pointers_gg"></span><span id="DDK_DRAWING_COLOR_POINTERS_GG"></span>


モノクロのポインターと同じ方法で、色のポインターを定義する (つまり、AND 部分と XOR 部分--を含むビットマップとして次のように表示します[ポインターの描画](pointer-drawing.md)と[モノクロ ポインターの描画](drawing-monochrome-pointers.md)) も。透過性と反転をサポートしています。

-   カラー ビットマップは黒 (インデックス 0) と、マスクの値が 1 の場合、結果は透明度です。

-   カラー ビットマップは白、およびマスクの値は 1、場合、結果は反転します。

-   デバイスが色を表示できない場合、白と黒としてのポインターを描画できます。

これらの規則は、色とモノクロの両方のディスプレイの 1 つのポインターの定義を使用するアプリケーションを許可します。

 

 





