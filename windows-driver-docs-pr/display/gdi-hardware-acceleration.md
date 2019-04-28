---
title: GDI ハードウェア アクセラレータ
description: GDI ハードウェア アクセラレータ
ms.assetid: 03db58e6-a6d5-4b6f-ba71-d22a985f9c57
keywords:
- ミニポート ドライバー WDK ディスプレイ
- GDI ハードウェア アクセラレータ WDK の表示
- 接続と構成が表示されます (CCD) WDK の表示
- GDI WDK ディスプレイを使用したハードウェア高速化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a6ec582440317c85574b81987c5405065f3366f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363846"
---
# <a name="gdi-hardware-acceleration"></a>GDI ハードウェア アクセラレータ


Windows 7 で導入された GDI ハードウェア アクセラレータ機能は、高速コア グラフィックス グラフィックス処理装置 (GPU) でデバイス インターフェイス (GDI) の操作を提供します。

GPU とドライバーは、この機能をサポート、ディスプレイのミニポート ドライバーが DXGKDDI を設定する必要がありますのことを示す\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN7 します。

ディスプレイのミニポート ドライバーも設定する必要があります[ **DXGK\_PRESENTATIONCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562004)-&gt;**SupportKernelModeCommandBuffer****TRUE**を GDI ハードウェア アクセラレータ コマンド バッファー処理をサポートしていることを示します。 ドライバーは、キャッシュの一貫性のある GPU aperture セグメントが存在して、CPU、GPU のメモリにアクセスすると、大幅なパフォーマンスの低下がない場合にのみ、この種のサポートを報告する必要があります。

以下の参照トピックでは、この機能を使用する方法について説明します。

<span id="Driver-Implemented_Functions"></span><span id="driver-implemented_functions"></span><span id="DRIVER-IMPLEMENTED_FUNCTIONS"></span>**ドライバー実装関数**  
次の関数は、GDI ハードウェア高速化をサポートする表示ミニポート ドライバーによって実装する必要があります。

[**DxgkDdiCreateAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff559606)

[**DxgkDdiGetStandardAllocationDriverData**](https://msdn.microsoft.com/library/windows/hardware/ff559673)

[**DxgkDdiRenderKm**](https://msdn.microsoft.com/library/windows/hardware/ff559800)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**構造体**
[**D3DKM\_TRANSPARENTBLTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff548468)

[**D3DKMDT\_GDISURFACEDATA**](https://msdn.microsoft.com/library/windows/hardware/ff546021)

[**D3DKMDT\_GDISURFACEFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff546031)

[**ドライバー\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff556169)

[**DXGK\_CREATECONTEXTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff561037)

[**DXGK\_CREATEDEVICEFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff561039)

[**DXGK\_GDIARG\_ALPHABLEND**](https://msdn.microsoft.com/library/windows/hardware/ff561074)

[**DXGK\_GDIARG\_BITBLT 関数**](https://msdn.microsoft.com/library/windows/hardware/ff561079)

[**DXGK\_GDIARG\_CLEARTYPEBLEND**](https://msdn.microsoft.com/library/windows/hardware/ff561082)

[**DXGK\_GDIARG\_COLORFILL**](https://msdn.microsoft.com/library/windows/hardware/ff561083)

[**DXGK\_GDIARG\_STRETCHBLT**](https://msdn.microsoft.com/library/windows/hardware/ff561089)

[**DXGK\_GDIARG\_TRANSPARENTBLT**](https://msdn.microsoft.com/library/windows/hardware/ff561091)

[**DXGK\_RENDERKM\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff562026)

[**DXGK\_PRESENTATIONCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562004)

[**DXGKARG\_GETSTANDARDALLOCATIONDRIVERDATA**](https://msdn.microsoft.com/library/windows/hardware/ff557598)

[**DXGKARG\_レンダリング**](https://msdn.microsoft.com/library/windows/hardware/ff557648)

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**列挙体**
[**D3DKMDT\_STANDARDALLOCATION\_型**](https://msdn.microsoft.com/library/windows/hardware/ff546589)

[**D3DKMDT\_GDISURFACETYPE**](https://msdn.microsoft.com/library/windows/hardware/ff546039)

[**DXGK\_GDIROP\_BITBLT 関数**](https://msdn.microsoft.com/library/windows/hardware/ff561095)

[**DXGK\_GDIROP\_COLORFILL**](https://msdn.microsoft.com/library/windows/hardware/ff561102)

[**DXGK\_RENDERKM\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff562029)

ディスプレイ ミニポート ドライバーで GDI ハードウェア高速化を実装する方法の詳細については、次のトピックを参照してください。

[メモリ割り当てのピッチとサイズの設定](setting-the-size-and-pitch-of-the-memory-allocation.md)

[初期化と DMA バッファーの作成](initialization-and-dma-buffer-creation.md)

[操作を表示するためのオプションのサポートのレポート](reporting-optional-support-for-rendering-operations.md)

[カーネル モード コマンド バッファーをサポートしています。](supporting-kernel-mode-command-buffers.md)

[GDI ハードウェア アクセラレータによるレンダリング操作を指定します。](specifying-gdi-hardware-accelerated-rendering-operations.md)

 

 





