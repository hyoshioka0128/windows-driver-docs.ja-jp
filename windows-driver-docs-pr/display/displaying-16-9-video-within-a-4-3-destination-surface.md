---
title: 4 3 内で 16 9 のビデオを表示する宛先表面
description: 4 3 内で 16 9 のビデオを表示する宛先表面
ms.assetid: 8500ec9c-876d-4b94-a58a-2513942305db
keywords:
- 16 9 のビデオを表示します。
- 4 3 宛先表面 VA WDK DirectX を 16 9 ビデオを表示します。
- 16 9 ビデオ 4 3 で宛先表面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e31f9d83928a71628828d6e6416beccd4cf421e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538121"
---
# <a name="displaying-169-video-within-a-43-destination-surface"></a>4:3 変換先の画面内で 16:9 のビデオを表示します。


## <span id="ddk_displaying_16_9_video_within_a_4_3_destination_surface_gg"></span><span id="DDK_DISPLAYING_16_9_VIDEO_WITHIN_A_4_3_DESTINATION_SURFACE_GG"></span>


このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

次の例では、VMR が 4:3 変換先の画面内で 16:9 のビデオ ストリームを表示するように指示します。

![4:3 変換先の画面内で 16:9 のビデオを示す図](images/trgrect.png)

わかりやすくするための前の例が含まれていないこと、ビデオのサブストリームに注意してください。 前の例では、四角形は次のとおりです。

-   ターゲットの四角形 = {0, 0、640, 480}

-   ビデオ ストリーム:
    -   Source rectangle = {0, 0, 720, 480},
    -   先の四角形 = {0, 60,640,300}

 

 





