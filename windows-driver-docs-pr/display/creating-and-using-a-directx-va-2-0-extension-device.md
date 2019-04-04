---
title: 作成して、DirectX VA 2.0 の拡張機能のデバイスを使用します。
description: 作成して、DirectX VA 2.0 の拡張機能のデバイスを使用します。
ms.assetid: 650a77a5-67c3-4b11-93c8-24232905eb43
keywords:
- DirectX ビデオ アクセラレータ WDK の表示、拡張のサポート
- ビデオ アクセラレータ WDK DirectX、拡張のサポート
- VA WDK DirectX、拡張のサポート
- 拡張機能のデバイス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee104a279eaf8f80bf33dac35494d07356545cd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560875"
---
# <a name="creating-and-using-a-directx-va-20-extension-device"></a>作成して、DirectX VA 2.0 の拡張機能のデバイスを使用します。


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateExtensionDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540644) DirectX VA 2.0、拡張機能のデバイスを作成する関数。 ユーザー モードのディスプレイ ドライバーの呼び出し、デバイスで Direct3D ランタイムが終了したら、 [ **DestroyExtensionDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552774)関数。

Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **DecodeExtensionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551811)非標準のビデオをデコードする関数がデバイスとの間、開始フレームとフレームの終了時間帯をデコードします。特定のレンダー ターゲットのサーフェイス。 ビデオのデコードについての概要については、[ビデオのデコード](decoding-video.md)を参照してください。

Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **ExtensionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff565604)拡張機能のデバイスでの非標準の DirectX VA 2.0 操作を実行する関数。

 

 





