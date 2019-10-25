---
title: モーションベクター
description: モーションベクター
ms.assetid: 463a2434-7f3e-4960-a595-8ca2ccc21504
keywords:
- マクロが WDK DirectX VA、モーションベクターをブロックする
- モーションベクター WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ce9084609df3adadf74508d6c9b64cb2c3c34ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840552"
---
# <a name="motion-vectors"></a>モーションベクター


## <span id="ddk_motion_vectors_gly"></span><span id="DDK_MOTION_VECTORS_GLY"></span>


画像が画像内にない場合は ( **DXVA\_ピクチャパラメーター**または*P picture*の**bpicture** in メンバー)。 さらに、マクロブロックベースの参照画像の選択 (たとえば、「(263)」で定義されている) が使用されている場合は、各モーションベクターの参照画像選択インデックスも、マクロブロックコントロールコマンドの構造に含まれています。

各マクロブロックコントロールのコマンド構造で、モーションベクター用に予約された領域は、通常、4つのモーションベクターに必要な量です。 各モーションベクターは、 [**DXVA\_MVvalue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mvvalue)構造体を使用して指定されます。 これらの一般的なケースには、上記以外の2つのケースが含まれます。 残りのケース ( *dxva*ヘッダーファイルでは明示的に定義されていません) は次のとおりです。

-   *Obmc*が使用されている場合 ( [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**bpicture obmc**メンバーが 1)、画像が PB 画像の B 部分ではない (この構造体の**bpicture binpb**メンバーがゼロ)、10個のモーションベクター用の領域にプラス16バイトの境界に配置するために必要な追加の領域が含まれています。

-   OBMC が使用されている場合 (DXVA\_グラフィックパラメーター構造体の**Bpicture Obmc**メンバーが 1)、画像が PB 画像の B 部分である (この構造体の**Bpicture binpb**のメンバーは 1)、11モーションベクターの領域、および追加の領域が必要です。16バイトの境界に合わせて配置されます。

-   OBMC が使用されていない (DXVA\_ピクチャパラメーター構造体の**Bpicture Obmc**メンバーがゼロ) 場合、画像は PB 画像の B 部分 (この構造体の**Bpicture binpb**メンバーは 1) であり、マクロブロックごとに4つのモーションベクターが許可されます (この構造体の**bPic4Mvallowed**メンバーは 1) で、5つのモーションベクターの領域に加え、16バイトの境界に配置するために必要な追加の領域も含まれています。

 

 





