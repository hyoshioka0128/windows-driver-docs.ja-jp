---
title: ビデオ処理デバイスの作成
description: ビデオ処理デバイスの作成
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- ビデオ WDK DirectX VA を処理する、デバイスの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbccc35674a7f1531d321facaee55e6c93502976
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346925"
---
# <a name="creating-a-video-processing-device"></a>ビデオ処理デバイスの作成


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateVideoProcessDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540729)ビデオ ストリームを処理するためのデバイスを作成する関数。 ユーザー モードのディスプレイ ドライバーの呼び出し、デバイスで Direct3D ランタイムが終了したら、 [ **DestroyVideoProcessDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552814)関数。

 

 





