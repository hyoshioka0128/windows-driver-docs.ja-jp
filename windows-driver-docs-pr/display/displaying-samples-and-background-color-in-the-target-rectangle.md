---
title: ターゲットの四角形の色の表示のサンプルとバック グラウンド
description: 次のトピックでは、ターゲットの四角形に背景色でさまざまなサンプルを表示する方法を説明します。
ms.assetid: 324fa569-4b2e-4ee1-9988-d08020df78e9
keywords:
- DeinterlaceBltEx、ターゲットの四角形
- 対象の四角形の WDK DirectX VA
- 背景の色のオプション WDK DirectX VA
- WDK の DirectX va なので、ターゲットの四角形をデインター レース
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 954b0540f29d0007988cfaef50f21084a0920b65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553010"
---
# <a name="displaying-samples-and-background-color-in-the-target-rectangle"></a>ターゲットの四角形の色のサンプルと背景を表示します。


## <span id="ddk_displaying_samples_and_background_color_in_the_target_rectangle_gg"></span><span id="DDK_DISPLAYING_SAMPLES_AND_BACKGROUND_COLOR_IN_THE_TARGET_RECTANGLE_GG"></span>


このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

Windows XP SP2、Windows Server 2003 SP1 以降の VMR 後で、ビデオ ストリームとサブストリームを表示する方法を決定する、ターゲットの四角形と背景色を指定することができます。

VMR には、ドライバーが出力を出力する必要があります宛先表面内の場所を識別するために、ターゲットの四角形を指定します。 ソース四角形の座標は常にソース画面; 内で絶対の場所として指定します。同様に、移行先の四角形とターゲットの四角形の座標は、常に変換先の画面内で絶対の場所として指定します。 通常、ビデオ ストリームとサブストリームの元とコピー先の四角形は、ソースと宛先表面; と同じサイズただし、これとは限りません場合です。 詳細については、[処理 Subrectangles](processing-subrectangles.md)を参照してください。

次のトピックでは、ターゲットの四角形の背景色でさまざまなサンプルを表示する方法を示します。

[4:3 変換先の画面内で 16:9 のビデオを表示します。](displaying-16-9-video-within-a-4-3-destination-surface.md)

[Stream のビデオと縦横比が異なるとサブストリームの組み合わせ](combining-video-stream-and-substream-with-different-aspect-ratios.md)

[異なる高さと幅の 2 つのストリームを結合](combining-two-streams-with-different-heights-and-widths.md)

 

 





