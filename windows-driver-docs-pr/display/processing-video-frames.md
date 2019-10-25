---
title: ビデオ フレームの処理
description: ビデオ フレームの処理
ms.assetid: 0f613186-1887-4d67-95d6-f562124c69ab
keywords:
- ビデオ処理 WDK DirectX VA、ビデオフレーム処理
- ビデオフレーム処理 WDK DirectX VA
- WDK DirectX VA のフレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45fa57f90ea2636b530583ad8633136b4a4cf350
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826036"
---
# <a name="processing-video-frames"></a>ビデオ フレームの処理


Microsoft Direct3D ランタイムは、ユーザーモード display driver の[**Videoprocessbeginframe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessbeginframe)および[**videoprocessbeginframe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessendframe)関数を呼び出して、ユーザーモード display driver がビデオを処理できるこれらの関数呼び出しの間の期間を示します。連結. ユーザーモード表示ドライバーがビデオフレームを処理できるようにするには、Microsoft Direct3D ランタイムがユーザーモードの表示ドライバーの[**SetVideoProcessRenderTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setvideoprocessrendertarget)関数を呼び出して、ビデオ処理のレンダーターゲット画面を設定する必要があります。 ただし、 *SetVideoProcessRenderTarget*の呼び出しは、開始フレームと終了フレームの間にのみ発生します。

ビデオ処理のレンダーターゲットサーフェイスが設定されると、ユーザーモードの表示ドライバーは、その[**Videoprocessblt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessblt)関数への呼び出しを受信して、開始フレームと終了フレーム期間の間のビデオフレームを処理できます。

 

 





