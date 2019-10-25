---
title: ビデオ デコード デバイスの作成
description: ビデオ デコード デバイスの作成
ms.assetid: a9820da9-436f-40b7-a25d-3208600f7a2f
keywords:
- ビデオデコード WDK DirectX VA、デコードデバイスの作成
- ビデオをデコードする WDK DirectX VA、デコードデバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56659ae8a0e7ceb25d047aed98c0089ca9ae6fc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839777"
---
# <a name="creating-a-video-decode-device"></a>ビデオ デコード デバイスの作成


Microsoft Direct3D ランタイムは、ユーザーモードの表示ドライバーの[**CreateDecodeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice)関数を呼び出して、ビデオアクセラレータ (VA) のデコードデバイスを作成します。 デコードデバイスで Direct3D ランタイムが終了すると、ユーザーモードの表示ドライバーの[**DestroyDecodeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroydecodedevice)関数が呼び出されます。

 

 





