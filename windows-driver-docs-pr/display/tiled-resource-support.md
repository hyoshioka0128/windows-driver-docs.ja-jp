---
title: タイル表示されたリソースのサポート
description: タイル化されたリソースは、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでサポートされています。 この機能は Windows 8.1 以降の新機能です。
ms.assetid: 02F3DFB8-2407-412A-B518-9AF4A3E1466A
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 54c29ba8b6bb085a0ff466cb2c2d55470968c2d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825453"
---
# <a name="tiled-resource-support"></a>タイル表示されたリソースのサポート


タイル化されたリソースは、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでサポートされています。 この機能は Windows 8.1 以降の新機能です。

以下の参照トピックでは、ユーザーモードの表示ドライバーにこの機能を実装する方法について説明します。

* [**PFND3DWDDM1_3DDI_CHECKMULTISAMPLEQUALITYLEVELS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_checkmultisamplequalitylevels)
* [**PFND3DWDDM1_3DDI_COPYTILEMAPPINGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_copytilemappings)
* [**PFND3DWDDM1_3DDI_COPYTILES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_copytiles)
* [**PFND3DWDDM1_3DDI_GETMIPPACKING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_getmippacking)
* [**PFND3DWDDM1_3DDI_RELOCATEDEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_relocatedevicefuncs)
* [**PFND3DWDDM1_3DDI_RESIZETILEPOOL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_resizetilepool)
* [**PFND3DWDDM1_3DDI_TILEDRESOURCEBARRIER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_tiledresourcebarrier)
* [**PFND3DWDDM1_3DDI_UPDATETILEMAPPINGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_updatetilemappings)
* [**PFND3DWDDM1_3DDI_UPDATETILES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_updatetiles)
* [**D3DWDDM1\_3DDI\_チェック\_マルチサンプリング\_品質\_レベル\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_check_multisample_quality_levels_flag)
* [**D3DWDDM1\_3DDI\_D3D11\_オプション\_DATA1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_d3d11_options_data1)
* [**D3DWDDM1\_3DDI\_DEVICEFUNCS 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_devicefuncs)
* [**D3DWDDM1\_3DDI\_タイル\_コピー\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_copy_flag)
* [**D3DWDDM1\_3DDI\_タイル\_マッピング\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_mapping_flag)
* [**D3DWDDM1\_3DDI\_タイル\_範囲\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_range_flag)
* [**D3DWDDM1\_3DDI\_タイル\_領域\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_tile_region_size)
* [**D3DWDDM1\_3DDI\_タイル\_リソース\_座標**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_tiled_resource_coordinate)
* [**D3DWDDM1\_3DDI\_タイル\_リソース\_\_フラグをサポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tiled_resources_support_flag)
* [**D3D10\_2DDICAPS\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_2ddicaps_type) (**D3DWDDM1\_3ddicaps\_D3D11\_OPTIONS1**定数値)
* [**D3D10\_DDI\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_filter) (**D3DWDDM1\_3ddi\_filter\_XXX**定数値)
* [**D3D10\_DDI\_リソース\_その他の\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)(**D3DWDDM1\_3DDI\_リソース\_** その他\_タイル化された**D3DWDDM1\_3DDI\_リソース\_その他の\_タイル\_POOL**定数値)
* [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice) (**PWDDM1\_3DeviceFuncs 関数**メンバー)
* [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext) (**PWDDM1\_3contextfuncs**メンバー)

 

 





