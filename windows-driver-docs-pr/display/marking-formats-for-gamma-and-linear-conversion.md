---
title: ガンマと線形変換の形式をマークします。
description: ガンマと線形変換の形式をマークします。
ms.assetid: 1285b04e-b67a-46d2-82b2-3cde433bf578
keywords:
- ガンマ補正 WDK DirectX 9.0、ガンマ変換の形式をマークします。
- 変換 WDK DirectX 9.0 のフォーマットをマークします。
- 線形変換 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5939fbadf9cb4ea6ff5ab5fb22ca4b0257dbff6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550722"
---
# <a name="marking-formats-for-gamma-and-linear-conversion"></a>ガンマと線形変換の形式をマークします。


## <span id="ddk_marking_formats_for_gamma_and_linear_conversion_gg"></span><span id="DDK_MARKING_FORMATS_FOR_GAMMA_AND_LINEAR_CONVERSION_GG"></span>


DirectX 9.0 のバージョンのドライバーが線形のテクスチャ形式をマークまたはガンマ変換ことは、テクスチャの正確に処理またはそれらを表示するには、それらの形式に変換するかどうかを判断できるようにします。

テクスチャのコンテンツは通常、ガンマ補正がの sRGB 形式で格納されます。 ただし、ピクセル パイプラインのテクスチャの sRGB 形式での正確な描画操作を実行する場合、ドライバーする必要があります、テクスチャ形式に変換線形読み取る前にそこから。 ピクセルのパイプラインにそれらのテクスチャをレンダー ターゲットに書き込む準備ができたら、ドライバーは、sRGB 形式に戻す、テクスチャを変換する必要があります。 この方法では、ピクセルのパイプラインは、線形の領域のすべての操作を実行します。

ドライバーでは、次のフラグを指定します、 **dwOperations**のメンバー、 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)の形式をマークするテクスチャ サーフェスの形式の構造変換:

-   D3DFORMAT\_OP\_テクスチャは、ガンマ値 2.2 かどうかを修正するかどうかを示す SRGBREAD (sRGB かどうか) とにする必要があります形式に変換を線形ブレンド操作またはサンプラーのために、ドライバーによって参照時にします。

-   D3DFORMAT\_OP\_SRGBWRITE をピクセルがパイプラインかどうかする必要がありますガンマ補正を sRGB 領域、レンダー ターゲットを書き出すときを示します。

 

 





