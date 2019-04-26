---
title: DirectX VA 2.0 拡張デバイスの作成と使用
description: DirectX VA 2.0 拡張デバイスの作成と使用
ms.assetid: 650a77a5-67c3-4b11-93c8-24232905eb43
keywords:
- DirectX ビデオ アクセラレータ WDK の表示、拡張のサポート
- ビデオ アクセラレータ WDK DirectX、拡張のサポート
- VA WDK DirectX、拡張のサポート
- 拡張機能のデバイス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee104a279eaf8f80bf33dac35494d07356545cd5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346922"
---
# <a name="creating-and-using-a-directx-va-20-extension-device"></a>DirectX VA 2.0 拡張デバイスの作成と使用


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateExtensionDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540644) DirectX VA 2.0、拡張機能のデバイスを作成する関数。 ユーザー モードのディスプレイ ドライバーの呼び出し、デバイスで Direct3D ランタイムが終了したら、 [ **DestroyExtensionDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552774)関数。

Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **DecodeExtensionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551811)非標準のビデオをデコードする関数がデバイスとの間、開始フレームとフレームの終了時間帯をデコードします。特定のレンダー ターゲットのサーフェイス。 ビデオのデコードについての概要については、次を参照してください。[ビデオのデコード](decoding-video.md)します。

Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **ExtensionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff565604)拡張機能のデバイスでの非標準の DirectX VA 2.0 操作を実行する関数。

 

 





