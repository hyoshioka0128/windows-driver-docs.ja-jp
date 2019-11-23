---
title: GDI ハードウェア アクセラレータ
description: GDI ハードウェア アクセラレータ
ms.assetid: 03db58e6-a6d5-4b6f-ba71-d22a985f9c57
keywords:
- ミニポート ドライバー WDK ディスプレイ
- GDI ハードウェアアクセラレータ WDK ディスプレイ
- ディスプレイ (CCD) WDK ディスプレイの接続と構成
- GDI WDK ディスプレイを使用したハードウェア高速化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ec7e79a60714aa7c360082a66d4c816393989b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839685"
---
# <a name="gdi-hardware-acceleration"></a>GDI ハードウェア アクセラレータ


Windows 7 で導入された GDI ハードウェアアクセラレーション機能は、グラフィックスプロセッシングユニット (GPU) に高速なコアグラフィックスデバイスインターフェイス (GDI) 操作を提供します。

GPU とドライバーがこの機能をサポートしていることを示すには、ディスプレイミニポートドライバーで DXGKDDI\_INTERFACE\_VERSION を &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN7 に設定する必要があります。

また、ディスプレイミニポートドライバーでは、 [**DXGK\_プレゼンテーションキャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)-&gt;**SupportKernelModeCommandBuffer**を**TRUE**に設定して、GDI ハードウェアアクセラレーションコマンドバッファー処理がサポートされていることを示す必要があります。 ドライバーがこの種類のサポートを報告する必要があるのは、キャッシュ整合性のある GPU アパーチャセグメントが存在し、CPU が GPU メモリにアクセスしたときにパフォーマンスが大幅に低下しない場合のみです。

次の参照トピックでは、この機能の使用方法について説明します。

<span id="Driver-Implemented_Functions"></span><span id="driver-implemented_functions"></span><span id="DRIVER-IMPLEMENTED_FUNCTIONS"></span>**ドライバーによって実装される関数**  
次の関数は、GDI ハードウェアアクセラレータをサポートするディスプレイミニポートドライバーによって実装される必要があります。

[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)

[**DxgkDdiGetStandardAllocationDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)

[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**構造体**
[ **D3DKM\_TRANSPARENTBLTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_d3dkm_transparentbltflags)

[**D3DKMDT\_GDISURFACEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)

[**D3DKMDT\_GDISURFACEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfaceflags)

[**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)

[**DXGK\_CREATECONTEXTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_createcontextflags)

[**DXGK\_CREATEDEVICEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_createdeviceflags)

[**DXGK\_GDIARG\_ALPHABLEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend)

[**DXGK\_GDIARG\_BITBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt)

[**DXGK\_GDIARG\_CLEARTYPEBLEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend)

[**DXGK\_GDIARG\_COLORFILL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill)

[**DXGK\_GDIARG\_STRETCHBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt)

[**DXGK\_GDIARG\_TRANSPARENTBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt)

[**DXGK\_RENDERKM\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_renderkm_command)

[**DXGK\_のプレゼンテーションキャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)

[**DXGKARG\_GETSTANDARDの DRIVERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata)

[**DXGKARG\_RENDER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**列挙**
[ **D3DKMDT\_standardallocation\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_standardallocation_type)

[**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)

[**DXGK\_GDIROP\_BITBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_gdirop_bitblt)

[**DXGK\_GDIROP\_COLORFILL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_gdirop_colorfill)

[**DXGK\_RENDERKM\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_renderkm_operation)

ディスプレイミニポートドライバーに GDI ハードウェア高速化を実装する方法の詳細については、次のトピックを参照してください。

[メモリ割り当てのサイズとピッチの設定](setting-the-size-and-pitch-of-the-memory-allocation.md)

[初期化と DMA バッファーの作成](initialization-and-dma-buffer-creation.md)

[表示操作のオプションサポートを報告する](reporting-optional-support-for-rendering-operations.md)

[カーネルモードのコマンドバッファーのサポート](supporting-kernel-mode-command-buffers.md)

[GDI ハードウェアアクセラレータレンダリング操作の指定](specifying-gdi-hardware-accelerated-rendering-operations.md)

 

 





