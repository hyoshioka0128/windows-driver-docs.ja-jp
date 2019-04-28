---
title: WIA ビデオ ドライバーの開発
description: WIA ビデオ ドライバーの開発
ms.assetid: 3cf14fd3-1dfa-480e-a69c-c4d2c196a504
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0579d3db48d6e5943b24ee021711e89d620649d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364574"
---
# <a name="developing-a-wia-video-driver"></a>WIA ビデオ ドライバーの開発





ビデオやビデオ_カメラ WIA をサポートします。 ビデオ_カメラ WIA を使用することは、バージョンでは、Windows Me、Windows XP およびそれ以降のオペレーティング システムで出荷または DirectShow のビデオ ドライバーを開発するビデオ ドライバーを使用する必要があります。 WIA ビデオ ストリームからのイメージを引き続き取得する DirectShow に依存します。

DirectShow のドライバーの INF ファイルにのみ、いくつか変更は、wia がサポートされているカメラとして認識する必要があります。 必要な変更は次のとおりです。

```INF
[Device]
Include= sti.inf
Needs= STI.WIAVideo.Registration
SubClass=StillImage
DeviceType=3
DeviceSubType=0x1
Capabilities=0x00000031
ICMProfiles="sRGB Color Space Profile.icm"
```

これらの追加を行っていない場合は、WIA がデバイスを認識していません。 必ず*追加*INF ファイルにこれらの変更。 次の行のみ、INF ファイルを置き換えないでください。

サポートする方法の例には、ドライバーからまだ pin と USBCAMD モデルを使用してビデオ_カメラから WIA を参照してください[USB-Based カメラ キャプチャ ボタンで](https://msdn.microsoft.com/library/windows/hardware/ff568643)します。

 

 




