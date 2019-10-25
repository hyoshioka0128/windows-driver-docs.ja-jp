---
title: FOURCC としてのサーフェスの形式
description: FOURCC としてのサーフェスの形式
ms.assetid: 947b73c9-3f1d-485e-9966-815b40a06342
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、テクスチャ形式の一覧
- テクスチャ形式は、WDK DirectX 8.0 を一覧表示します
- Dピクセル形式
- surface 形式 WDK DirectX 8.0
- Fourcc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3f922ead72668f642f73be91bd0c5b7fff71afb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825520"
---
# <a name="surface-formats-as-fourccs"></a>FOURCC としてのサーフェスの形式


## <span id="ddk_surface_formats_as_fourccs_gg"></span><span id="DDK_SURFACE_FORMATS_AS_FOURCCS_GG"></span>


DirectX 8.0、D3DFMT\_Q8W8V8U8、D3DFMT\_V16U16、D3DFMT\_W11V11U10 で定義されている新しい表面の3つの形式は、ドライバーに4番目の*ccs*として渡されます。 これは、 [**Ddピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)のデータ構造体のさまざまなビットの深さフィールドとマスクフィールドが初期化されず、その値が未定義であることを意味します。 したがって、これら3つの形式を処理するドライバーは、ピクセル形式のビット数またはマスクに依存しないようにする必要がありますが、これらは必要に応じて計算する必要があります。 たとえば、これらのいずれかの種類のサーフェイスのピッチを計算する場合、ピクセル形式の**Dwrgbbitcount**フィールドは使用できません。 YUV、DXT、および IHV 固有の拡張形式以外の他のすべての形式は、ドライバーに渡されるときに従来の DDPIXEL 形式の表現にマップされます。したがって、ピクセル形式のデータ構造体に有効なピクセル形式とマスクがあります。

 

 





