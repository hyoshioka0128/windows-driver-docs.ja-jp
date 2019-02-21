---
title: ハードウェア アクセラレータ スライダーを表示します。
description: ハードウェア アクセラレータ スライダーを表示します。
ms.assetid: af3daa64-196a-4163-872d-713bc4cf0335
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デバッグ
- デバッグ ドライバー WDK Windows 2000 を表示します。
- ハードウェア アクセラレータ スライダー WDK Windows 2000 の表示
- アクセラレータ スライダーを WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74baba77a1777d602d5274a77437565e7fd76eb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558932"
---
# <a name="display-hardware-acceleration-slider"></a>ハードウェア アクセラレータ スライダーを表示します。


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

-   [**DrvStretchBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556302)

-   [**DrvPlgBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556258)

-   [**DrvFillPath**](https://msdn.microsoft.com/library/windows/hardware/ff556220)

-   [**DrvStrokeAndFillPath**](https://msdn.microsoft.com/library/windows/hardware/ff556311)

-   [**DrvLineTo**](https://msdn.microsoft.com/library/windows/hardware/ff556245)

-   [**DrvStretchBltROP**](https://msdn.microsoft.com/library/windows/hardware/ff556306)

-   [**DrvTransparentBlt**](https://msdn.microsoft.com/library/windows/hardware/ff557283)

-   [**DrvAlphaBlend**](https://msdn.microsoft.com/library/windows/hardware/ff556176)

-   [**DrvGradientFill**](https://msdn.microsoft.com/library/windows/hardware/ff556236)

<span id="Level_3"></span><span id="level_3"></span><span id="LEVEL_3"></span>**レベル 3**  
Microsoft DirectDraw、Direct3D のサポートを無効になっています。

<span id="Level_4"></span><span id="level_4"></span><span id="LEVEL_4"></span>**レベル 4**  
次のグラフィックス操作のみが高速化します。

-   [**DrvTextOut**](https://msdn.microsoft.com/library/windows/hardware/ff557277)

-   [**DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)

-   [**DrvCopyBits**](https://msdn.microsoft.com/library/windows/hardware/ff556182)

-   [**DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)

また、次のディスプレイ ドライバー関数は呼び出されません。

-   [**DrvSaveScreenBits**](https://msdn.microsoft.com/library/windows/hardware/ff556278)

-   [**DrvEscape**](https://msdn.microsoft.com/library/windows/hardware/ff556217)

-   [**DrvDrawEscape**](https://msdn.microsoft.com/library/windows/hardware/ff556203)

-   [**DrvResetPDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556276)

-   [**DrvSetPixelFormat**](https://msdn.microsoft.com/library/windows/hardware/ff556285)

-   [**DrvDescribePixelFormat**](https://msdn.microsoft.com/library/windows/hardware/ff556190)

-   [**DrvSwapBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff556322)

<span id="Level_5"></span><span id="level_5"></span><span id="LEVEL_5"></span>**レベル 5**  
スライダーは左端の位置です。 パンのドライバー (カーネル モードの GDI の一部) は、すべてのレンダリングを処理します。 GDI の呼び出し、ディスプレイ ドライバーの[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)と[ **DrvEnableSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff556214)プライマリ画面を作成する関数し、も呼び出します表示モードを設定する、ディスプレイ ドライバー。 ディスプレイ ドライバーは、レンダリングを行うには呼び出されません。

ハードウェア アクセラレータの表示を制限する別の方法がでフラグを設定するには、 **CapabilityOverride**レジストリ エントリ。 たとえば 0x2 フラグを設定、 **CapabilityOverride**エントリはレベル 3 にハードウェア アクセラレータ スライダーを配置するのと同じです。 説明については、 **CapabilityOverride**レジストリ エントリを参照してください[INF ファイルのセクションでは表示](display-inf-file-sections.md)します。

 

 





