---
title: カーネル モード ビデオ トランスポートの使用
description: カーネル モード ビデオ トランスポートの使用
ms.assetid: 0be84371-f7d5-42bb-b164-80fcf1b58d95
keywords:
- カーネルモードのビデオトランスポート WDK DirectDraw、カーネルモードのビデオトランスポートについて
- DirectDraw カーネルモード video transport WDK Windows 2000 display、カーネルモードビデオトランスポートについて
- カーネルモードビデオトランスポート WDK DirectDraw、カーネルモードビデオトランスポートについて
- ビデオトランスポートカーネルモード WDK DirectDraw、カーネルモードビデオトランスポートについて
- ビデオキャプチャ WDK ビデオトランスポートのカーネルモード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0ea774ffb91d4b021fc112c2cfa46a265a527fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825396"
---
# <a name="using-kernel-mode-video-transport"></a>カーネル モード ビデオ トランスポートの使用


## <span id="ddk_using_kernel_mode_video_transport_gg"></span><span id="DDK_USING_KERNEL_MODE_VIDEO_TRANSPORT_GG"></span>


カーネルモードのビデオトランスポート機能は、 *dxapi .lib*とリンクする[ビデオキャプチャドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)によってアクセスされます。これにより、後で*dxapi .sys*を呼び出すことができます。 この機能は、DirectDraw が読み込まれている場合にのみ使用できます。

ビデオキャプチャドライバー (ハードウェアデコーダー用) は、カーネルモード DirectDraw に付属している[**dxapi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)関数を使用して、dxapi インターフェイスのコールバック関数にアクセスします。 **Dxapi**関数は、関数識別子、入力バッファーとサイズ、および出力バッファーとサイズを受け取る1つのエントリポイントです。 この関数の動作と、入力バッファーと出力バッファーのサイズと形式は、指定された関数識別子によって異なります。 **Dxapi**関数とその関数識別子は、 *ddkmapi. h*で定義されています。

DirectShow または別のクライアントは、DirectDraw 経由でビデオミニポートドライバーによって提供される DxApi インターフェイスコールバック関数にアクセスします。 DxApi インターフェイスのコールバック関数は、 *dxapi .h*で定義されています。

カーネルモードのビデオトランスポートインターフェイスを使用するには、ビデオキャプチャドライバーが、使用する必要がある各 DirectDraw オブジェクト、surface、および VPE オブジェクトのユーザーモードハンドルを受け取る必要があります。 キャプチャモデルと MPEG モデルでは、これらのハンドルは既存の Api を使用して渡されます。 ドライバーがストリームクラスドライバーではなく、この機能を必要とする場合、ユーザーモードコンポーネントは[Idirectdrawkernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)インターフェイスと[IDirectDrawSurfaceKernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) COM インターフェイスを使用してハンドルを取得し、ドライバーに渡すことができます。 COM インターフェイスとそのメソッドは、 *ddkernel .h*で識別されます。

 

 





