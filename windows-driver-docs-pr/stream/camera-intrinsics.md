---
title: カメラの組み込み
description: カメラの組み込み関数についてを説明します。
ms.date: 09/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 06081bc39204298abdf8899239d31d9fa1e6de9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370496"
---
# <a name="camera-intrinsics"></a>カメラの組み込み

カメラのドライバー (または代わりに、DMFT を通じて) か、属性ストアを使用してストリームにカメラの組み込みの属性をアタッチできる[MFStreamExtension_PinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/medfound/mfstreamextension-pinholecameraintrinsics)、メディア フレーム属性ストアを使用して、にアタッチまたは[MFSampleExtension_PinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/medfound/mfsampleextension-pinholecameraintrinsics)します。 ストリームの属性ストアにアタッチされている場合、カメラの組み込みの値はカメラのストリーミング中には変わりません。 アタッチされている場合、メディア、属性ストアのフレーム組み込み値では、すべてのフレームが変わる可能性があります。 

上記の 2 つの属性の値が型の構造体をする必要があります[MFPinholeCameraIntrinsics](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-_mfpinholecameraintrinsics)カメラの組み込みのモデルの一覧を報告します。 このリストの各エントリは型[MFPinholeCameraIntrinsic_IntrinsicModel](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-mfpinholecameraintrinsic_intrinsicmodel)、解像度 (幅/高さ)、一モデルでは、格納されていると[MFCameraIntrinsic_DistortionModel](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-_mfcameraintrinsic_distortionmodel)ゆがみモデル. 

使用する場合**MFPinholeCameraIntrinsics**ストリーム属性ストアでは、この一覧には、少なくとも 1 つと可能性がある多くの組み込みモデルも含まれて 必要があります。 システムでは、幅と高さのフレームを照合することによって積極的にストリーミングのフレーム形式に基づく組み込みのモデルを選択します。 完全一致が見つかった場合は、組み込み関数が使用されます。 それ以外の場合、最初の付いた組み込み縦横比をされる代わりに、たとえば、それぞれ一覧に、640 x 480 と 1920 x 1080 の 2 つのエントリが含まれている場合。 1280 x 720 メディア形式のストリーミング、1080 p 組み込み関数は適切なスケーリングを併用します。 

使用する場合**MFPinholeCameraIntrinsics**メディア フレームの属性ストアでは、この一覧がフレームの解像度と同じ解像度に 1 つの組み込みモデルを含める必要があります。
