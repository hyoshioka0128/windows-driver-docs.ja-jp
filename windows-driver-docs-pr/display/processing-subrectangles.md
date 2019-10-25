---
title: サブ矩形の処理
description: サブ矩形の処理
ms.assetid: d00803c0-98e2-4101-bcfc-ef11fea07962
keywords:
- WDK DirectX VA、subrectangular 処理のノンインターレース化
- subrectangular 処理 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3623e9df308fbb75a44a4d1cd2a98d02cae70a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829677"
---
# <a name="processing-subrectangles"></a>サブ矩形の処理


## <span id="ddk_processing_subrectangles_gg"></span><span id="DDK_PROCESSING_SUBRECTANGLES_GG"></span>


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

Windows Server 2003 SP1 以降および Windows XP SP2 以降の VMR では、ソースビデオイメージとビデオサブストリームのサブ四角形領域を処理し、ターゲットサーフェイスのサブ四角形領域に書き込むことができます。 VMR は、 [**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体の**rcsrc**メンバーと**rcsrc**メンバーの四角形の座標を、それぞれのサンプルの座標とは異なるものにすることによって、サブ四角形の処理操作を実行します。コピー元とコピー先のサーフェイス。

インターレース化されていないハードウェアがサブ四角形プロセスの操作をサポートしている場合、表示ドライバーは、\_DXVA の**Videoprocessingcaps**メンバーで DXVA\_videoprocess\_SubRects フラグを設定することによって、このサポートを報告します。 [**DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体。 このドライバーは、 [**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)関数が呼び出されたときに、DXVA\_DeinterlaceCaps へのポインターを返します。

サブ四角形を処理する操作では、VMR はサブ四角形を伸縮でき、ターゲットサーフェイスでサブ四角形を相互に交差させることができます。

次のトピックでは、さまざまなサブ四角形プロセス操作を実行する方法について説明します。

[拡大せずにサブ四角形を処理する](processing-subrectangles-without-stretching.md)

[拡大 (サブ四角形を)](stretching-subrectangles.md)

 

 





