---
title: モーション ベクトル
description: モーション ベクトル
ms.assetid: 463a2434-7f3e-4960-a595-8ca2ccc21504
keywords:
- WDK の DirectX va なので、動きベクトルをマクロ ブロック
- 動きベクトル WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1692ceb4dff47464663f1ba8ae251c51a4e17ae4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574738"
---
# <a name="motion-vectors"></a>モーション ベクトル


## <span id="ddk_motion_vectors_gly"></span><span id="DDK_MOTION_VECTORS_GLY"></span>


画像が、内の画像ではない場合 (、 **bPicIntra**のメンバー、 **DXVA\_PictureParameters**または*P 画像*)。 さらに、マクロ ブロック ベースの参照を画像の選択 (で定義されている H.263 Annex U) を使用している場合、各動きベクトルの参照画像の選択範囲のインデックスも含まれますマクロ ブロック コントロール コマンド構造体。

各マクロ ブロック コントロール コマンドの構造に動きベクトルの予約済みの領域は、一般に、モーションの 4 つのベクトルに必要な量です。 使用して各動きベクトルを指定する[ **DXVA\_MVvalue** ](https://msdn.microsoft.com/library/windows/hardware/ff564004)構造体。 通常このような場合に、前の 2 つの nonintra ケースが含まれます。 残りのケース (で明示的に定義されている、 *dxva.h*ヘッダー ファイル) は次のようにします。

-   場合*OBMC*使用されています (、 **bPicOBMC**のメンバー、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造体が 1) 画像PB 画像の B 部分ではありません (、 **bPicBinPB**この構造体のメンバーは 0 です)、10 個の動きベクトル + 16 バイト境界に合わせるために必要な追加領域をスペースが含まれています。

-   OBMC を使用している場合 (、 **bPicOBMC**メンバーは、DXVA の\_PictureParameters 構造は 1) PB 図の B の一部であり、画像 (、 **bPicBinPB**この構造体のメンバーは 1)、11 用の領域モーションのベクトルと、16 バイト境界に合わせるために必要な追加の領域が含まれます。

-   OBMC が使用されていない場合 (、 **bPicOBMC** 、DXVA のメンバー\_PictureParameters 構造体は 0 です)、画像は PB 図の B 部分 (、 **bPicBinPB**この構造体のメンバーは 1)、または 4 つマクロ ブロックごとの動きベクトルが許可されている (、 **bPic4Mvallowed**この構造体のメンバーは 1)、5 つの動きベクトルと、16 バイト境界に合わせるために必要な追加の領域の容量が含まれています。

 

 





