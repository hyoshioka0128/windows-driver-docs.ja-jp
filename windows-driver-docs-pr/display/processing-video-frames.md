---
title: ビデオ フレームの処理
description: ビデオ フレームの処理
ms.assetid: 0f613186-1887-4d67-95d6-f562124c69ab
keywords:
- ビデオの処理の WDK DirectX va なので、ビデオ フレームの処理
- ビデオのフレームの WDK DirectX VA の処理
- フレームの WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41dc0b882706c6ed115bc73e134f27f43cc4c58b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363702"
---
# <a name="processing-video-frames"></a>ビデオ フレームの処理


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **VideoProcessBeginFrame** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessbeginframe)と[ **VideoProcessEndFrame** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessendframe)ユーザー モードのディスプレイ ドライバーでビデオ フレームが処理できるこれらの関数呼び出しまでの時間を示す関数。 ユーザー モードのディスプレイ ドライバーは、ビデオのフレームを処理できますが、前に、マイクロソフトの Direct3D ランタイムは、ユーザー モードのディスプレイ ドライバーを呼び出す必要があります[ **SetVideoProcessRenderTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setvideoprocessrendertarget)レンダリングを設定する関数ビデオの処理のための画面をターゲット。 ただし、呼び出し*SetVideoProcessRenderTarget*期間開始フレーム、終了フレーム以外にのみ発生することができます。

レンダー ターゲットのサーフェスの後に、ビデオの処理が設定されて、ユーザー モードのディスプレイ ドライバー通話を受信できるにその[ **VideoProcessBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessblt)開始フレーム間のビデオのフレームを処理する関数と期間の終了-フレーム。

 

 





