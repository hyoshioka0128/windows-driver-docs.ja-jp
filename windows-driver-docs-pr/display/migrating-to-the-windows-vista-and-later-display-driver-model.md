---
title: Windows Display Driver Model (WDDM) への移行
description: Windows Display Driver Model (WDDM) への移行
ms.assetid: 7f926aa7-1698-4a4e-a1ce-54a316bdc0cd
keywords:
- ドライバー モデル WDK Windows Vista では、表示を移行します。
- Windows Vista のディスプレイ ドライバー モデル、WDK を移行します。
- 移行のディスプレイ ドライバー モデル WDK Windows Vista
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8c3ddc55b14c0dd69257c4c34014228e02f1960
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379860"
---
# <a name="migrating-to-the-windows-display-driver-model-wddm"></a>Windows Display Driver Model (WDDM) への移行


## <span id="ddk_migrating_to_the_longhorn_display_driver_model_gg"></span><span id="DDK_MIGRATING_TO_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


Windows 表示 Driver Model (WDDM) への移行) には、完全に別の表示とビデオのミニポート ドライバーを記述するためにドライバー作成者が必要です。 ような[Windows 2000 display driver model (XDDM)](windows-2000-display-driver-model-design-guide.md)WDDM が、ペアになっている必要がありますドライバーが表示されミニポート ドライバーを表示します。 ただし、WDDM、ディスプレイ ドライバーはユーザー モードで実行します。 また、モデルが、Windows グラフィックス デバイス インターフェイス (GDI) エンジンのサービスを使用しませんモデルでは、マイクロソフトの Direct3D ランタイムおよび Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) のサービスを使用します。

WDDM は、表示と XDDM に従って記述されたビデオのミニポート ドライバーをサポートします。 ただし、新しいドライバーが可能であれば、Windows Vista 以降で利用可能なソフトウェアとハードウェアの機能を活用するために、WDDM ドライバーとして書き込まれます。

新しいデバイス ドライバー インターフェイス (DDI) を書き直す必要がありますが、ドライバーの作成者は、WDDM ドライバーでの低レベルのハードウェアに依存するコードを再利用できるの関連コードです。 WDDMdrivers を記述する場合は、これらの点を考慮します。

-   ディスプレイのミニポート ドライバーでは、改訂された一連のオペレーティング システムおよび DirectX グラフィックスのカーネル サブシステムと対話するエントリ ポイント関数を実装する必要があります。 詳細については、次を参照してください。 [**ディスプレイ ミニポート ドライバーの DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)します。 ディスプレイのミニポート ドライバーでは、任意の文書化されているカーネル関数を呼び出すことができます。

-   ディスプレイのミニポート ドライバーは、適切な DirectX グラフィックスのカーネル サブシステムを動的に読み込みます。 ディスプレイのミニポート ドライバーと DirectX グラフィックスのカーネル サブシステム インターフェイスを介して相互に呼び出します。

-   ディスプレイのミニポート ドライバーでは、最もビデオの (IOCTL) I/O 制御コードを処理する必要なくなりました。 XDDM でカーネル モードのディスプレイ ドライバーは、ビデオのミニポート ドライバーとの通信にこれらのコードを使用します。 WDDM、ユーザー モードのディスプレイ ドライバーは、Direct3D ランタイムと通信します。WDDM グラフィックスのカーネル サブシステムは、ディスプレイのミニポート ドライバーと通信します。
    **注**  次 Ioctl は、WDDM で引き続き使用して、ディスプレイのミニポート ドライバーが処理する必要があります。[**IOCTL\_ビデオ\_クエリ\_色\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities)
    [**IOCTL\_ビデオ\_ハンドル\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

     

<!-- -->

-   ユーザー モードのディスプレイ ドライバーを実装およびエクスポートする必要があります、 [ **OpenAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)関数で、グラフィックス アダプターのインスタンスを開きます。 ユーザー モードのディスプレイ ドライバーを実装する必要がありますも、 [ **CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)関数で、表示状態のコレクションを処理するディスプレイ デバイスの表現を作成します。

-   ユーザー モードのディスプレイ ドライバーの[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数、ディスプレイのミニポート ドライバーのと共に[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数を置き換える、 [ *DdCanCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))、 [ *DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))、および[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) XDDM で機能します。

-   ほとんどの残りのユーザー モード ディスプレイ ドライバー関数は、XDDM 用のカーネル モードのディスプレイ ドライバーが次のように実装されるのと同じ機能を実装します。
    -   [ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数と[ **DP2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation)操作コード
    -   [補正コールバック関数のモーション](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と[DirectX ビデオ アクセラレータ構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

 

 





