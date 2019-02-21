---
title: 動き補正コールバック
description: 動き補正コールバック
ms.assetid: a1f748e4-0d62-4543-a409-bb9ec02a7d77
keywords:
- 描画の WDK DirectDraw、動き補正
- DirectDraw WDK Windows 2000 の表示、動き補正
- 動き補正 WDK
- 圧縮されたビデオのデコード WDK DirectDraw
- ビデオのデコード WDK DirectDraw
- WDK DirectDraw をデコード
- コールバック関数の WDK DirectDraw 動き補正
- デジタル ビデオのデコード WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8252c7ce899166483e6b9e3d38569747df59134
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551422"
---
# <a name="motion-compensation-callbacks"></a>動き補正コールバック


## <span id="ddk_motion_compensation_callbacks_gg"></span><span id="DDK_MOTION_COMPENSATION_CALLBACKS_GG"></span>


[DirectX のビデオ アクセラレータ](directx-video-acceleration.md)DirectDraw でデジタル ビデオ デコーディングの高速化用のドライバーを処理するこのようなアルファ ブレンドのサポートを目的として DVD として提供される次の動き補正のコールバック関数の使用サブピクチャ サポート:

[*DdMoCompBeginFrame*](https://msdn.microsoft.com/library/windows/hardware/ff549648)

[*DdMoCompCreate*](https://msdn.microsoft.com/library/windows/hardware/ff549656)

[*DdMoCompDestroy*](https://msdn.microsoft.com/library/windows/hardware/ff549664)

[*DdMoCompEndFrame*](https://msdn.microsoft.com/library/windows/hardware/ff549669)

[*DdMoCompGetBuffInfo*](https://msdn.microsoft.com/library/windows/hardware/ff549683)

[*DdMoCompGetFormats*](https://msdn.microsoft.com/library/windows/hardware/ff549691)

[*DdMoCompGetGuids*](https://msdn.microsoft.com/library/windows/hardware/ff550236)

[*DdMoCompGetInternalInfo*](https://msdn.microsoft.com/library/windows/hardware/ff550240)

[*DdMoCompQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff550243)

[*DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)

動き補正のコールバック関数には、DirectX ビデオ アクセラレータ インターフェイスのデバイス ドライバーの側が構成されています。 動き補正のコールバック関数がのメンバーで指定された、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。 次の手順では、モーション補正のコールバック関数へのアクセス方法を示しています。

1.  Guid から受信した**IAMVideoAccelerator::GetVideoAcceleratorGUIDs** 、デバイス ドライバーの由来[ *DdMoCompGetGuids*](https://msdn.microsoft.com/library/windows/hardware/ff550236)します。

2.  ダウン ストリームの入力ピン呼び出し**IAMVideoAccelerator::GetUncompFormatsSupported**から、デバイス ドライバーのデータを返す[ *DdMoCompGetFormats*](https://msdn.microsoft.com/library/windows/hardware/ff549691)します。

3.  関連の処理の開始時、 [ **DXVA\_ConnectMode** ](https://msdn.microsoft.com/library/windows/hardware/ff563138)データ構造体のデコーダーの出力ピンが**IAMVideoAcceleratorNotify:。GetCreateVideoAcceleratorData** 、デバイス ドライバーに渡される[ *DdMoCompCreate*](https://msdn.microsoft.com/library/windows/hardware/ff549656)、ビデオ アクセラレータ オブジェクトのデコーダーを通知します。

4.  返されるデータ**IAMVideoAccelerator::GetCompBufferInfo** 、デバイス ドライバーの発生元[ *DdMoCompGetBuffInfo*](https://msdn.microsoft.com/library/windows/hardware/ff549683)します。

5.  使用して送信バッファー **IAMVideoAccelerator::Execute** 、デバイス ドライバーのによって受信されて[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)します。

6.  使用**IAMVideoAccelerator::QueryRenderStatus**呼び出し、デバイス ドライバーの[ *DdMoCompQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff550243)します。 DDERR のリターン コード\_から WASSTILLDRAWING *DdMoCompQueryStatus* E のリターン コードとしてホスト デコーダーによって表示されるように\_から PENDING **IAMVideoAccelerator::QueryRenderStatus**.

7.  送信されるデータ**IAMVideoAccelerator::BeginFrame**を受信したデバイス ドライバーの[ *DdMoCompBeginFrame*](https://msdn.microsoft.com/library/windows/hardware/ff549648)します。 DDERR のリターン コード\_から WASSTILLDRAWING が必要な*DdMoCompBeginFrame* E の順序で\_への応答で、ホストのデコーダーで認識されるに保留**IAMVideoAccelerator::BeginFrame**.

8.  送信されるデータ**IAMVideoAccelerator::EndFrame**を受信したデバイス ドライバーの[ *DdMoCompEndFrame*](https://msdn.microsoft.com/library/windows/hardware/ff549669)します。

9.  関連する処理、デバイス ドライバーの末に[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)ドライバーに通知する現在のビデオ アクセラレータ オブジェクトは使用されなく、ドライバーが実行できるようにするために使用必要なクリーンアップします。

 

 





