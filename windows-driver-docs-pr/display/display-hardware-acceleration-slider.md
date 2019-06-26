---
title: ディスプレイ ハードウェア アクセラレータ スライダー
description: ディスプレイ ハードウェア アクセラレータ スライダー
ms.assetid: af3daa64-196a-4163-872d-713bc4cf0335
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デバッグ
- デバッグ ドライバー WDK Windows 2000 を表示します。
- ハードウェア アクセラレータ スライダー WDK Windows 2000 の表示
- アクセラレータ スライダーを WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2944969d1aea7a719ca5f80dc38a3d1e9da1d4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385193"
---
# <a name="display-hardware-acceleration-slider"></a>ディスプレイ ハードウェア アクセラレータ スライダー


## <span id="ddk_display_hardware_acceleration_slider_gg"></span><span id="DDK_DISPLAY_HARDWARE_ACCELERATION_SLIDER_GG"></span>


**プロパティの表示**ダイアログ ボックスのディスプレイ ドライバーをデバッグするときに役に立つハードウェア アクセラレータ スライダーがあります。 スライダーを使用すると、6 つのレベルをレベル 0 (アクセラレータ) からレベル 5 (アクセラレータなし) に至るまでのいずれかにディスプレイ ハードウェアの高速化のサポートを設定できます。

Microsoft Windows XP では、ハードウェア アクセラレータ スライダーを見つけるには開きます、**表示プロパティ** ダイアログ ボックスをクリックして、**設定**タブ。をクリックして、 **詳細設定**ボタンをクリックし、をクリックし、**トラブルシューティング**タブ。

次の一覧には、各レベルで無効になっているハードウェア アクセラレータの一部について説明します。 後続のすべてのレベルでは、特定のレベルで無効になっているすべての機能が無効です。

<span id="Level_0"></span><span id="level_0"></span><span id="LEVEL_0"></span>**レベル 0**  
スライダーは、一番右の位置にあります。 ハードウェア アクセラレータが完全に有効にします。

<span id="Level_1"></span><span id="level_1"></span><span id="LEVEL_1"></span>**レベル 1**  
ハードウェアのカーソルとデバイスにビットマップのサポートが無効になります。

<span id="Level_2"></span><span id="level_2"></span><span id="LEVEL_2"></span>**レベル 2**  
次のディスプレイ ドライバー関数は呼び出されません。 代わりに、GDI では、ソフトウェアの操作を実行します。

-   [**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)

-   [**DrvPlgBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)

-   [**DrvFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)

-   [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)

-   [**DrvLineTo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)

-   [**DrvStretchBltROP**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)

-   [**DrvTransparentBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)

-   [**DrvAlphaBlend**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)

-   [**DrvGradientFill**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)

<span id="Level_3"></span><span id="level_3"></span><span id="LEVEL_3"></span>**レベル 3**  
Microsoft DirectDraw、Direct3D のサポートを無効になっています。

<span id="Level_4"></span><span id="level_4"></span><span id="LEVEL_4"></span>**レベル 4**  
次のグラフィックス操作のみが高速化します。

-   [**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)

-   [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)

-   [**DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)

-   [**DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)

また、次のディスプレイ ドライバー関数は呼び出されません。

-   [**DrvSaveScreenBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsavescreenbits)

-   [**DrvEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)

-   [**DrvDrawEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape)

-   [**DrvResetPDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)

-   [**DrvSetPixelFormat**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)

-   [**DrvDescribePixelFormat**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat)

-   [**DrvSwapBuffers**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvswapbuffers)

<span id="Level_5"></span><span id="level_5"></span><span id="LEVEL_5"></span>**レベル 5**  
スライダーは左端の位置です。 パンのドライバー (カーネル モードの GDI の一部) は、すべてのレンダリングを処理します。 GDI の呼び出し、ディスプレイ ドライバーの[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)と[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)プライマリ画面を作成する関数し、も呼び出します表示モードを設定する、ディスプレイ ドライバー。 ディスプレイ ドライバーは、レンダリングを行うには呼び出されません。

ハードウェア アクセラレータの表示を制限する別の方法がでフラグを設定するには、 **CapabilityOverride**レジストリ エントリ。 たとえば 0x2 フラグを設定、 **CapabilityOverride**エントリはレベル 3 にハードウェア アクセラレータ スライダーを配置するのと同じです。 説明については、 **CapabilityOverride**レジストリ エントリを参照してください[INF ファイルのセクションでは表示](display-inf-file-sections.md)します。

 

 





