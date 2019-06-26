---
title: ビデオ処理デバイスの作成
description: ビデオ処理デバイスの作成
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- ビデオ WDK DirectX VA を処理する、デバイスの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d7ca4ae86f624ebba7734a6b88781c62e890c30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370227"
---
# <a name="creating-a-video-processing-device"></a>ビデオ処理デバイスの作成


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateVideoProcessDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createvideoprocessdevice)ビデオ ストリームを処理するためのデバイスを作成する関数。 ユーザー モードのディスプレイ ドライバーの呼び出し、デバイスで Direct3D ランタイムが終了したら、 [ **DestroyVideoProcessDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyvideoprocessdevice)関数。

 

 





