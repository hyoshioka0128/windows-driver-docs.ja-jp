---
title: ビデオ デコード デバイスの作成
description: ビデオ デコード デバイスの作成
ms.assetid: a9820da9-436f-40b7-a25d-3208600f7a2f
keywords:
- ビデオのデコード WDK DirectX VA はデバイスをデコードを作成します。
- ビデオの WDK DirectX VA をデコードするには、デバイスのデコードを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40b7a1c45f920982d4bc9f34eba620d57e30bfb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370232"
---
# <a name="creating-a-video-decode-device"></a>ビデオ デコード デバイスの作成


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateDecodeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice)ビデオ アクセラレータ (VA) のデコード デバイスを作成する関数。 ユーザー モードのディスプレイ ドライバーのデコード デバイスで Direct3D ランタイムが終了したら、呼び出す[ **DestroyDecodeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroydecodedevice)関数。

 

 





