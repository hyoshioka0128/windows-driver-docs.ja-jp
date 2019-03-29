---
title: ジョイスティック ドライバー モデル
description: ジョイスティック ドライバー モデル
ms.assetid: 5bd41377-37ae-4ca7-8a6d-93311511ef4e
keywords:
- ジョイスティックに WDK を非表示にドライバー モデル
- 仮想ジョイスティックのドライバー WDK を非表示にドライバー モデル
- VJoyD WDK HID、ドライバー モデル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bceba0389623f9c6c3a5bfce7181a3cab9e60cb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574970"
---
# <a name="joystick-driver-model"></a>ジョイスティック ドライバー モデル





ジョイスティックの情報をタイムリーにアクセスを提供すること、ジョイスティック ドライバー モデルの最も重要な目標の 1 つです。 2 つのドライバーが Windows 95/98/Me ジョイスティックのサービスを提供します。 16 ビット リング 3 ドライバー (Msjstick.drv) と 32 ビット リング 0 ドライバー (Vjoyd.vxd)。 Msjstick.drv ドライバーは、レジストリの更新プログラムや cap 情報; などの基本的なサービスを提供します。Vjoyd.vxd は、ポーリングのサービスを提供します。

ジョイスティックの API は、Windows 95/98/Me、および 32 ビット アプリケーションの Winmm.dll DLL から 16 ビット アプリケーションの Mmsystem.dll ダイナミック リンク ライブラリ (DLL) によって提供されます。 Msjstick.drv ジョイスティックのすべてのサービスの通信 Mmsystem.dll (Msjstick.drv 通信 Vjoyd.vxd ポーリングのサービスを提供する)。 Winmm.dll は、ポーリング サービスは、Vjoyd.vxd と直接通信し、タイム クリティカルではない基本的なサービスの Mmsystem.dll するサンクします。

DirectX 5.0、DirectInput を開始し、COM ベースの代替 API を提供します。 Dinput.dll VJoyD を使用して、使用可能な場合ヒューマン インターフェイス デバイス (HID) スタック、ポーリングのサービスを提供します。 HID デバイスは、古い API を使用するアプリケーションが新しいデバイスの読み取りもできないようににも VJoyD を介して報告されます。 、Dinput.dll、または拡張の VJoyD ミニドライバーによって読み込まれる DLL であることがあり、OEM によって提供されるドライバーは、フォース フィードバックを処理します。

 

 




