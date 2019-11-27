---
title: Windows Display Driver Model (WDDM) への移行
description: Windows Display Driver Model (WDDM) への移行
ms.assetid: 7f926aa7-1698-4a4e-a1ce-54a316bdc0cd
keywords:
- ドライバーモデルの表示 WDK Windows Vista、移行
- Windows Vista display driver model WDK、移行
- 表示ドライバーモデルの移行 WDK Windows Vista
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 730b408074c3d01e69b8504f540a780b413e5032
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840570"
---
# <a name="migrating-to-the-windows-display-driver-model-wddm"></a>Windows Display Driver Model (WDDM) への移行


## <span id="ddk_migrating_to_the_longhorn_display_driver_model_gg"></span><span id="DDK_MIGRATING_TO_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


Windows Display Driver Model (WDDM) に移行するには、ドライバーの作成者がまったく異なる表示とビデオミニポートドライバーを書き込む必要があります。 [Windows 2000 display driver model (XDDM)](windows-2000-display-driver-model-design-guide.md)と同様に、WDDM には、ペアリングされたディスプレイドライバーとミニポートドライバーが必要です。 ただし、WDDM では、ディスプレイドライバーはユーザーモードで実行されます。 また、モデルは Windows グラフィックスデバイスインターフェイス (GDI) エンジンのサービスを使用しません。このモデルでは、Microsoft Direct3D ランタイムと Microsoft DirectX graphics カーネルサブシステム (Dxgkrnl) のサービスを使用します。

WDDM は、XDDM に従って記述された表示およびビデオミニポートドライバーをサポートしています。 ただし、Windows Vista 以降で利用できるソフトウェアとハードウェアの機能を利用するには、可能な限り、新しいドライバーを WDDM ドライバーとして記述する必要があります。

ドライバー作成者は WDDM ドライバーで低レベルのハードウェアに依存するコードを再利用できますが、新しいデバイスドライバーインターフェイス (DDI) 関連のコードを書き換える必要があります。 WDDMdrivers を作成する場合は、次の点を考慮してください。

-   ディスプレイミニポートドライバーは、オペレーティングシステムと DirectX グラフィックスカーネルサブシステムと対話するために、変更されたエントリポイント関数のセットを実装する必要があります。 詳細については、「 [**Driverentry Of Display ミニポートドライバー**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)」を参照してください。 表示ミニポートドライバーは、ドキュメント化されたカーネル関数を呼び出すことができます。

-   ディスプレイミニポートドライバーは、適切な DirectX グラフィックスのカーネルサブシステムを動的に読み込みます。 ディスプレイミニポートドライバーと DirectX グラフィックスサブシステムは、インターフェイスを介して互いに呼び出します。

-   ほとんどのビデオ i/o 制御コード (IOCTL) を処理するために、表示ミニポートドライバーは不要になりました。 XDDM では、カーネルモードのディスプレイドライバーは、これらのコードを使用してビデオミニポートドライバーと通信します。 WDDM では、ユーザーモード表示ドライバーは Direct3D ランタイムと通信します。WDDM グラフィックスカーネルサブシステムは、ディスプレイミニポートドライバーと通信します。
    **ただし**、次のような IOCTL が WDDM で使用されていて、ディスプレイミニポートドライバーでそれらを処理する必要がある   に注意してください。 IOCTL [ **\_video\_クエリ\_色\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities) [**ioctl
    ビデオ\_VIDEOPARAMETERS\_の処理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)\_

     

<!-- -->

-   ユーザーモード表示ドライバーは、 [**openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)関数を実装してエクスポートする必要があります。これにより、グラフィックスアダプターのインスタンスが開かれます。 ユーザーモード表示ドライバーは、レンダリング状態のコレクションを処理するディスプレイデバイスの表現を作成する[**CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)関数も実装する必要があります。

-   ユーザーモード表示ドライバーの[**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数と、ディスプレイミニポートドライバーの[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数を使用して、Xddm 内の[*ddcan urface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))、 [*ddD3dCreateSurfaceEx urface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))、および[](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)関数を置き換えます。

-   残りのユーザーモード表示ドライバー関数のほとんどは、次のように、XDDM 用のカーネルモード表示ドライバーと同じ機能を実装しています。
    -   [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数と[**DP2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)操作コード
    -   [モーション補正コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)と[DirectX ビデオアクセラレータ構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 





