---
title: カーネル モード ビデオ トランスポートの使用
description: カーネル モード ビデオ トランスポートの使用
ms.assetid: 0be84371-f7d5-42bb-b164-80fcf1b58d95
keywords:
- 描画カーネル モードのビデオ トランスポート WDK DirectDraw、カーネル モードのビデオ トランスポートについて
- カーネル モードのビデオ トランスポートに関する、DirectDraw カーネル モードのビデオ トランスポート WDK Windows 2000 の表示します。
- カーネル モードのビデオ トランスポートに関するビデオ トランスポート WDK DirectDraw、カーネル モード
- ビデオ トランスポートのカーネル モードの WDK DirectDraw、カーネル モードのビデオ トランスポートについて
- ビデオ キャプチャ WDK ビデオ トランスポート カーネル モード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 098a93d572c31fd2de16be8e3a31d6c815a1a985
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372019"
---
# <a name="using-kernel-mode-video-transport"></a>カーネル モード ビデオ トランスポートの使用


## <span id="ddk_using_kernel_mode_video_transport_gg"></span><span id="DDK_USING_KERNEL_MODE_VIDEO_TRANSPORT_GG"></span>


カーネル モードのビデオ トランスポート機能にアクセスを[ビデオ キャプチャ ドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)とのリンクを*dxapi.lib*に後で呼び出しを許可する*dxapi.sys*します。 この機能は、DirectDraw が読み込まれるときにのみ使用できます。

ビデオ キャプチャ ドライバー (ハードウェア デコーダー) を使用して、 [ **DxApi** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxapi/nf-dxapi-dxapi) DxApi インターフェイスのコールバック関数にアクセスするカーネル モード DirectDraw で提供される関数。 **DxApi**関数は、関数の識別子、入力バッファーとサイズ、および、出力バッファーとサイズを受け入れる 1 つのエントリ ポイント。 この関数の入力と出力バッファーの形式とサイズの動作は、指定された関数の識別子に依存します。 **DxApi**関数とその関数の識別子で定義されます*ddkmapi.h*します。

DirectShow または別のクライアントは、DirectDraw、ビデオのミニポート ドライバーによって提供される DxApi インターフェイスのコールバック関数にアクセスします。 DxApi インターフェイスのコールバック関数が定義されている*dxmini.h*します。

カーネル モードのビデオ トランスポート インターフェイスを使用するには、場合は、ビデオ キャプチャ ドライバーに DirectDraw オブジェクト、画面、および使用する必要がある VPE オブジェクトのユーザー モードのハンドルを受信してする必要があります。 キャプチャと MPEG モデルでは、これらのハンドル、既存の Api を使用して渡されます。 ユーザー モード コンポーネントを使用してハンドルを取得できる場合は、ドライバーは、この機能が必要ですが、ストリーム クラス ドライバーではない、 [IDirectDrawKernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と[IDirectDrawSurfaceKernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) COM インターフェイスドライバーに渡します。 COM インターフェイスとそのメソッドがで識別される*ddkernel.h*します。

 

 





