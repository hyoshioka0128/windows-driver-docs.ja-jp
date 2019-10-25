---
title: DirectX VA 2.0 拡張デバイスの作成と使用
description: DirectX VA 2.0 拡張デバイスの作成と使用
ms.assetid: 650a77a5-67c3-4b11-93c8-24232905eb43
keywords:
- DirectX ビデオアクセラレーション WDK ディスプレイ、拡張サポート
- ビデオアクセラレーション WDK DirectX、拡張サポート
- VA WDK DirectX、拡張サポート
- 拡張機能デバイス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a26e8c0e09b86d5c6dd62d9f36d2d757468b3381
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839025"
---
# <a name="creating-and-using-a-directx-va-20-extension-device"></a>DirectX VA 2.0 拡張デバイスの作成と使用


Microsoft Direct3D ランタイムは、DirectX VA 2.0 用の拡張機能デバイスを作成するために、ユーザーモードの表示ドライバーの[**Createextensiondevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createextensiondevice)関数を呼び出します。 デバイスで Direct3D ランタイムが終了すると、ユーザーモードの display driver の[**Destroyextensiondevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyextensiondevice)関数が呼び出されます。

Direct3D ランタイムは、ユーザーモードの表示ドライバーの[**DecodeExtensionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)関数を呼び出して、非標準のデコードデバイス上のビデオを、開始フレームと終了フレーム期間と特定のレンダーターゲットサーフェイスとの間でデコードします。 ビデオのデコードに関する一般的な説明については、「[ビデオのデコード](decoding-video.md)」を参照してください。

Direct3D ランタイムは、拡張デバイスで非標準の DirectX VA 2.0 操作を実行するために、ユーザーモードの表示ドライバーの[**Extensionexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_extensionexecute)関数を呼び出します。

 

 





