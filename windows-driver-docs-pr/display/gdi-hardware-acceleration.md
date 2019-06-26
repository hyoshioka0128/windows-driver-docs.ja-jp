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
ms.openlocfilehash: 7755e6dd1cd415b0388e22875e893b896f614de8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354744"
---
# <a name="gdi-hardware-acceleration"></a>GDI ハードウェア アクセラレータ


Windows 7 で導入された GDI ハードウェア アクセラレータ機能は、高速コア グラフィックス グラフィックス処理装置 (GPU) でデバイス インターフェイス (GDI) の操作を提供します。

GPU とドライバーは、この機能をサポート、ディスプレイのミニポート ドライバーが DXGKDDI を設定する必要がありますのことを示す\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN7 します。

ディスプレイのミニポート ドライバーも設定する必要があります[ **DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)-&gt;**SupportKernelModeCommandBuffer** **TRUE**を GDI ハードウェア アクセラレータ コマンド バッファー処理をサポートしていることを示します。 ドライバーは、キャッシュの一貫性のある GPU aperture セグメントが存在して、CPU、GPU のメモリにアクセスすると、大幅なパフォーマンスの低下がない場合にのみ、この種のサポートを報告する必要があります。

以下の参照トピックでは、この機能を使用する方法について説明します。

<span id="Driver-Implemented_Functions"></span><span id="driver-implemented_functions"></span><span id="DRIVER-IMPLEMENTED_FUNCTIONS"></span>**ドライバー実装関数**  
次の関数は、GDI ハードウェア高速化をサポートする表示ミニポート ドライバーによって実装する必要があります。

[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)

[**DxgkDdiGetStandardAllocationDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)

[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**構造体**
[**D3DKM\_TRANSPARENTBLTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_d3dkm_transparentbltflags)

[**D3DKMDT\_GDISURFACEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)

[**D3DKMDT\_GDISURFACEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfaceflags)

[**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)

[**DXGK\_CREATECONTEXTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_createcontextflags)

[**DXGK\_CREATEDEVICEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_createdeviceflags)

[**DXGK\_GDIARG\_ALPHABLEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend)

[**DXGK\_GDIARG\_BITBLT 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt)

[**DXGK\_GDIARG\_CLEARTYPEBLEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend)

[**DXGK\_GDIARG\_COLORFILL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill)

[**DXGK\_GDIARG\_STRETCHBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt)

[**DXGK\_GDIARG\_TRANSPARENTBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt)

[**DXGK\_RENDERKM\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_renderkm_command)

[**DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)

[**DXGKARG\_GETSTANDARDALLOCATIONDRIVERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata)

[**DXGKARG\_レンダリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**列挙体**
[**D3DKMDT\_STANDARDALLOCATION\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_standardallocation_type)

[**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)

[**DXGK\_GDIROP\_BITBLT 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_gdirop_bitblt)

[**DXGK\_GDIROP\_COLORFILL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_gdirop_colorfill)

[**DXGK\_RENDERKM\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_renderkm_operation)

ディスプレイ ミニポート ドライバーで GDI ハードウェア高速化を実装する方法の詳細については、次のトピックを参照してください。

[メモリ割り当てのピッチとサイズの設定](setting-the-size-and-pitch-of-the-memory-allocation.md)

[初期化と DMA バッファーの作成](initialization-and-dma-buffer-creation.md)

[操作を表示するためのオプションのサポートのレポート](reporting-optional-support-for-rendering-operations.md)

[カーネル モード コマンド バッファーをサポートしています。](supporting-kernel-mode-command-buffers.md)

[GDI ハードウェア アクセラレータによるレンダリング操作を指定します。](specifying-gdi-hardware-accelerated-rendering-operations.md)

 

 





