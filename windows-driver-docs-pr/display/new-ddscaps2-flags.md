---
title: 新しい DDSCAPS2 フラグ
description: 新しい DDSCAPS2 フラグ
ms.assetid: a5171865-7339-422f-8470-154a0aadc496
keywords:
- Windows 2000 の WDK の表示、プレゼンテーションの DirectX 8.0 リリース ノートします。
- WDK DirectX 8.0 のプレゼンテーション
- レンダリング結果表示の WDK DirectX 8.0
- 表示される結果 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9938243a85570bd1bdcb85e5ef95200bdc7ed24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345553"
---
# <a name="new-ddscaps2-flags"></a>新しい DDSCAPS2 フラグ


## <span id="ddk_new_ddscaps2_flags_gg"></span><span id="DDK_NEW_DDSCAPS2_FLAGS_GG"></span>


新しいフラグを DDSCAPS2\_バック バッファーの維持が必要ないことを示す、DISCARDBACKBUFFER が導入されています。 D3DSWAPEFFECT アプリケーションを設定した場合に、プライマリの画面およびバック バッファーに設定されている\_の破棄、**存在**API。

DX8 ランタイムは別の新しいフラグ DDSCAPS2 を設定するようになりました\_NOTUSERLOCKABLE、プライマリ レプリカと反転のチェーンはロックがない場合は、バック バッファーまたは lockable でないすべてのレンダー ターゲットにします。 これにより、ドライバー、シーンの最適化の背後にあるためです。 ドライバーは、このような場合を処理する必要がありますが、このようなロックが低くても、高速を予期していないため、サーフェスをロックすることも可能であるに注意してください。

ドライバーが、/深度ステンシル バッファーが、DDSCAPS2 の存在によってロックできるかどうかを判断できますも\_NOTUSERLOCKABLE フラグ。

 

 





