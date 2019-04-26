---
title: ビデオ デコード デバイスの作成
description: ビデオ デコード デバイスの作成
ms.assetid: a9820da9-436f-40b7-a25d-3208600f7a2f
keywords:
- ビデオのデコード WDK DirectX VA はデバイスをデコードを作成します。
- ビデオの WDK DirectX VA をデコードするには、デバイスのデコードを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36d730edde511cf927c786959c9d1062def722f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346928"
---
# <a name="creating-a-video-decode-device"></a>ビデオ デコード デバイスの作成


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateDecodeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540618)ビデオ アクセラレータ (VA) のデコード デバイスを作成する関数。 ユーザー モードのディスプレイ ドライバーのデコード デバイスで Direct3D ランタイムが終了したら、呼び出す[ **DestroyDecodeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552757)関数。

 

 





