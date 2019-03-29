---
title: VPE とカーネル モード ビデオ トランスポートのアーキテクチャ
description: VPE とカーネル モード ビデオ トランスポートのアーキテクチャ
ms.assetid: 7264932a-7fe9-4ffe-bd25-b5cd605739fa
keywords:
- 描画のカーネル モード ビデオ トランスポート WDK DirectDraw、アーキテクチャ
- DirectDraw カーネル モードのビデオ トランスポート アーキテクチャ、Windows 2000 の WDK の表示
- カーネル モードのビデオ トランスポート WDK DirectDraw、アーキテクチャ
- ビデオ トランスポートのカーネル モードの WDK DirectDraw、アーキテクチャ
- ビデオ キャプチャ WDK ビデオ トランスポート カーネル モード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cd23ec90f61319e2cf5a6df301f6d9ccf610685
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581895"
---
# <a name="vpe-and-kernel-mode-video-transport-architecture"></a>VPE とカーネル モード ビデオ トランスポートのアーキテクチャ


## <span id="ddk_vpe_and_kernel_mode_video_transport_architecture_gg"></span><span id="DDK_VPE_AND_KERNEL_MODE_VIDEO_TRANSPORT_ARCHITECTURE_GG"></span>


このセクションでは、Windows 2000 およびビデオ ポートの拡張機能 (VPE) とカーネル モードのビデオ トランスポート DirectX 5.0 およびそれ以降のバージョンでの以降のアーキテクチャについての詳細を提供します。 カーネル モードのビデオ トランスポートのアーキテクチャは、Microsoft がデバイスに依存しないコードとして追加する新しい関数に基づきます。 カーネル モードのビデオ トランスポートから成る、 [ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364) DirectDraw の一部として提供されている機能、[ビデオのミニポート ドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)、および提供する COM インターフェイス メソッドDirectDraw の一部として。

### <a name="span-idwindows2000andlaterspanspan-idwindows2000andlaterspanwindows-2000-and-later"></a><span id="windows_2000_and_later"></span><span id="WINDOWS_2000_AND_LATER"></span>Windows 2000 以降

Windows 2000 以降では、次の図に示すように、DxApi コールバックの一部である、[ビデオのミニポート ドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)します。

![windows 2000 カーネル モードのビデオ トランスポート アーキテクチャを示す図します。](images/ddfg011.png)

DxApi コールバックの詳細については、次を参照してください。 [DxApi ミニポート ドライバーの機能の Windows 2000 以降](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)します。

上記の図は、その他のカーネル モードとユーザー モード コンポーネント (点線は、カーネル遷移を表します) との関連カーネル モードのビデオ トランスポート アーキテクチャを示します。 DirectShow (または別のユーザー モードのクライアント) を呼び出す、このアーキテクチャでは、 [IDirectDrawKernel](https://msdn.microsoft.com/library/windows/hardware/ff567398)と[IDirectDrawSurfaceKernel](https://msdn.microsoft.com/library/windows/hardware/ff567409) DirectDraw COM インターフェイスの DirectDraw オブジェクトへのハンドルを取得し、画面のオブジェクト。

**注**   MPEG と VGA デバイス間のデータ フローの PCI バスを使用してこのアーキテクチャもサポートします。

 

Windows 2000 以降では、クライアントは、ミニポート ドライバーにこれらのハンドルを渡します。 これらのハンドルは、カーネル モードのビデオ トランスポートへの呼び出しで指定されます。 次の図は、ユーザー モードとカーネル モードのビデオ トランスポートでのハンドルを渡す方法の簡易バージョンです。

![ハンドルが windows 2000 のビデオ トランスポートに渡すことを示す図](images/ddfg012.png)

 

 





