---
title: モーション補正コールバック
description: モーション補正コールバック
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
ms.openlocfilehash: ea8fdc7311a6466368cbe6880bcbb6eecb091e29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372871"
---
# <a name="motion-compensation-callbacks"></a>モーション補正コールバック


## <span id="ddk_motion_compensation_callbacks_gg"></span><span id="DDK_MOTION_COMPENSATION_CALLBACKS_GG"></span>


[DirectX のビデオ アクセラレータ](directx-video-acceleration.md)DirectDraw でデジタル ビデオ デコーディングの高速化用のドライバーを処理するこのようなアルファ ブレンドのサポートを目的として DVD として提供される次の動き補正のコールバック関数の使用サブピクチャ サポート:

[*DdMoCompBeginFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)

[*DdMoCompCreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)

[*DdMoCompDestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)

[*DdMoCompEndFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)

[*DdMoCompGetBuffInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)

[*DdMoCompGetFormats*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)

[*DdMoCompGetGuids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)

[*DdMoCompGetInternalInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getinternalinfo)

[*DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)

[*DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)

動き補正のコールバック関数には、DirectX ビデオ アクセラレータ インターフェイスのデバイス ドライバーの側が構成されています。 動き補正のコールバック関数がのメンバーで指定された、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 次の手順では、モーション補正のコールバック関数へのアクセス方法を示しています。

1.  Guid から受信した**IAMVideoAccelerator::GetVideoAcceleratorGUIDs** 、デバイス ドライバーの由来[ *DdMoCompGetGuids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)します。

2.  ダウン ストリームの入力ピン呼び出し**IAMVideoAccelerator::GetUncompFormatsSupported**から、デバイス ドライバーのデータを返す[ *DdMoCompGetFormats*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)します。

3.  関連の処理の開始時、 [ **DXVA\_ConnectMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_connectmode)データ構造体のデコーダーの出力ピンが**IAMVideoAcceleratorNotify:。GetCreateVideoAcceleratorData** 、デバイス ドライバーに渡される[ *DdMoCompCreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)、ビデオ アクセラレータ オブジェクトのデコーダーを通知します。

4.  返されるデータ**IAMVideoAccelerator::GetCompBufferInfo** 、デバイス ドライバーの発生元[ *DdMoCompGetBuffInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)します。

5.  使用して送信バッファー **IAMVideoAccelerator::Execute** 、デバイス ドライバーのによって受信されて[ *DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)します。

6.  使用**IAMVideoAccelerator::QueryRenderStatus**呼び出し、デバイス ドライバーの[ *DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)します。 DDERR のリターン コード\_から WASSTILLDRAWING *DdMoCompQueryStatus* E のリターン コードとしてホスト デコーダーによって表示されるように\_から PENDING **IAMVideoAccelerator::QueryRenderStatus**.

7.  送信されるデータ**IAMVideoAccelerator::BeginFrame**を受信したデバイス ドライバーの[ *DdMoCompBeginFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)します。 DDERR のリターン コード\_から WASSTILLDRAWING が必要な*DdMoCompBeginFrame* E の順序で\_への応答で、ホストのデコーダーで認識されるに保留**IAMVideoAccelerator::BeginFrame**.

8.  送信されるデータ**IAMVideoAccelerator::EndFrame**を受信したデバイス ドライバーの[ *DdMoCompEndFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)します。

9.  関連する処理、デバイス ドライバーの末に[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)ドライバーに通知する現在のビデオ アクセラレータ オブジェクトは使用されなく、ドライバーが実行できるようにするために使用必要なクリーンアップします。

 

 





