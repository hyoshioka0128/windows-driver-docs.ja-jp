---
title: VPE とカーネル モード ビデオ トランスポートのアーキテクチャ
description: VPE とカーネル モード ビデオ トランスポートのアーキテクチャ
ms.assetid: 7264932a-7fe9-4ffe-bd25-b5cd605739fa
keywords:
- カーネルモードのビデオトランスポート WDK DirectDraw、アーキテクチャ
- DirectDraw カーネルモード video transport WDK Windows 2000 ディスプレイ、アーキテクチャ
- カーネルモードのビデオトランスポート WDK DirectDraw、アーキテクチャ
- video transport カーネルモード WDK DirectDraw、アーキテクチャ
- ビデオキャプチャ WDK ビデオトランスポートのカーネルモード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 330a615d182c21eb0df322fd6ce4fcc2a80503fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825264"
---
# <a name="vpe-and-kernel-mode-video-transport-architecture"></a>VPE とカーネル モード ビデオ トランスポートのアーキテクチャ


## <span id="ddk_vpe_and_kernel_mode_video_transport_architecture_gg"></span><span id="DDK_VPE_AND_KERNEL_MODE_VIDEO_TRANSPORT_ARCHITECTURE_GG"></span>


このセクションでは、DirectX 5.0 以降のバージョンでのビデオポート拡張機能 (VPE) とカーネルモードのビデオトランスポートについて、Windows 2000 以降のアーキテクチャについて詳しく説明します。 カーネルモードのビデオトランスポートのアーキテクチャは、Microsoft がデバイスに依存しないコードとして追加した新しい関数に基づいています。 カーネルモードのビデオトランスポートは、DirectDraw の一部として提供される[**Dxapi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)関数、[ビデオミニポートドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)、および directdraw の一部として提供される COM インターフェイスメソッドで構成されています。

### <a name="span-idwindows_2000_and_laterspanspan-idwindows_2000_and_laterspanwindows-2000-and-later"></a><span id="windows_2000_and_later"></span><span id="WINDOWS_2000_AND_LATER"></span>Windows 2000 以降

Windows 2000 以降では、次の図に示すように、DxApi コールバックは[ビデオミニポートドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)の一部です。

![windows 2000 カーネルモードのビデオトランスポートアーキテクチャを示す図](images/ddfg011.png)

DxApi のコールバックの詳細については、「 [Windows 2000 以降用の Dxapi ミニポートドライバー関数](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)」を参照してください。

上の図は、他のカーネルモードおよびユーザーモードコンポーネントに関連するカーネルモードのビデオトランスポートアーキテクチャを示しています (破線は、カーネルの遷移を示しています)。 このアーキテクチャでは、DirectShow (または別のユーザーモードクライアント) が[Idirectdrawkernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)および[IDirectDrawSurfaceKernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) directdraw COM インターフェイスを呼び出して、directdraw オブジェクトと surface オブジェクトへのハンドルを取得します。

**注**   このアーキテクチャでは、MPEG デバイスと VGA デバイス間のデータフローに PCI バスを使用することもできます。

 

Windows 2000 以降では、クライアントはこれらのハンドルをミニポートドライバーに渡します。 これらのハンドルは、カーネルモードのビデオトランスポートの呼び出しで指定されます。 次の図は、ユーザーとカーネルモードのビデオトランスポートでハンドルが渡される方法の単純なバージョンを示しています。

![windows 2000 ビデオ転送を渡すハンドルを示す図](images/ddfg012.png)

 

 





