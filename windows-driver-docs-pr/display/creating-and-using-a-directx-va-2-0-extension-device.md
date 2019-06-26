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
ms.openlocfilehash: 6a1547c9016d02e3bba756d0cc12a29ae07b455a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370204"
---
# <a name="creating-and-using-a-directx-va-20-extension-device"></a>DirectX VA 2.0 拡張デバイスの作成と使用


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **CreateExtensionDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createextensiondevice) DirectX VA 2.0、拡張機能のデバイスを作成する関数。 ユーザー モードのディスプレイ ドライバーの呼び出し、デバイスで Direct3D ランタイムが終了したら、 [ **DestroyExtensionDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyextensiondevice)関数。

Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **DecodeExtensionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)非標準のビデオをデコードする関数がデバイスとの間、開始フレームとフレームの終了時間帯をデコードします。特定のレンダー ターゲットのサーフェイス。 ビデオのデコードについての概要については、次を参照してください。[ビデオのデコード](decoding-video.md)します。

Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **ExtensionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_extensionexecute)拡張機能のデバイスでの非標準の DirectX VA 2.0 操作を実行する関数。

 

 





