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
ms.openlocfilehash: d8f91269cc59dfb7f01eb9cb7203ce6e5e91bb71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370174"
---
# <a name="processing-video-frames"></a>ビデオ フレームの処理


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **VideoProcessBeginFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff570494)と[ **VideoProcessEndFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff570497)ユーザー モードのディスプレイ ドライバーでビデオ フレームが処理できるこれらの関数呼び出しまでの時間を示す関数。 ユーザー モードのディスプレイ ドライバーは、ビデオのフレームを処理できますが、前に、マイクロソフトの Direct3D ランタイムは、ユーザー モードのディスプレイ ドライバーを呼び出す必要があります[ **SetVideoProcessRenderTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff569695)レンダリングを設定する関数ビデオの処理のための画面をターゲット。 ただし、呼び出し*SetVideoProcessRenderTarget*期間開始フレーム、終了フレーム以外にのみ発生することができます。

レンダー ターゲットのサーフェスの後に、ビデオの処理が設定されて、ユーザー モードのディスプレイ ドライバー通話を受信できるにその[ **VideoProcessBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff570495)開始フレーム間のビデオのフレームを処理する関数と期間の終了-フレーム。

 

 





