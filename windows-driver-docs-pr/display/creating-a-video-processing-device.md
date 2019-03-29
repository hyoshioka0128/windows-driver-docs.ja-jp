---
title: ビデオ処理デバイスの作成
description: ビデオ処理デバイスの作成
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- ビデオ WDK DirectX VA を処理する、デバイスの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbccc35674a7f1531d321facaee55e6c93502976
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580540"
---
# <a name="creating-a-video-processing-device"></a>ビデオ処理デバイスの作成


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateVideoProcessDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540729)ビデオ ストリームを処理するためのデバイスを作成する関数。 ユーザー モードのディスプレイ ドライバーの呼び出し、デバイスで Direct3D ランタイムが終了したら、 [ **DestroyVideoProcessDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552814)関数。

 

 





