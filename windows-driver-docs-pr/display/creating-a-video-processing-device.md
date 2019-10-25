---
title: ビデオ処理デバイスの作成
description: ビデオ処理デバイスの作成
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- ビデオ処理 WDK DirectX VA、デバイスの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f649f90d8d93ee143e763ad4c73f4fcfa5658e17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839775"
---
# <a name="creating-a-video-processing-device"></a>ビデオ処理デバイスの作成


Microsoft Direct3D ランタイムは、ユーザーモードの表示ドライバーの[**Createvideoprocessdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createvideoprocessdevice)関数を呼び出して、ビデオストリームを処理するためのデバイスを作成します。 デバイスで Direct3D ランタイムが終了すると、ユーザーモードの表示ドライバーの[**Destroyvideoprocessdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyvideoprocessdevice)関数が呼び出されます。

 

 





