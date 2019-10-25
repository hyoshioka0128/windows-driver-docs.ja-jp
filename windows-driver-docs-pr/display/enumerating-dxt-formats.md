---
title: DXT 形式の列挙
description: DXT 形式の列挙
ms.assetid: 77fc961f-1b94-43c1-b238-86f7d8e96835
keywords:
- 圧縮されたテクスチャの描画 WDK DirectDraw、DXT 形式の列挙
- DirectDraw 圧縮テクスチャ WDK Windows 2000 display、DXT 形式の列挙
- 圧縮されたテクスチャサーフェス WDK DirectDraw、DXT 形式の列挙
- WDK DirectDraw、圧縮されたテクスチャを表面にします
- テクスチャ WDK DirectDraw、圧縮
- DXT 形式の列挙 WDK DirectDraw
- DXT 形式 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a791e32ca3954acee0b1e49f52f56d76959968fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838949"
---
# <a name="enumerating-dxt-formats"></a>DXT 形式の列挙


## <span id="ddk_enumerating_dxt_formats_gg"></span><span id="DDK_ENUMERATING_DXT_FORMATS_GG"></span>


Microsoft DirectX には、ドライバーがピクセル形式を列挙するための2つの方法があります。 最初のメソッドは、テクスチャに使用できる形式を列挙します。 このメソッドは、 [**D3DHAL\_GLOBALDRIVERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)構造体の**lpTextureFormats**メンバーを使用して実装されます。 2番目のメソッドは、DDSCAPS\_オーバーレイサーフェスまたは DDSCAPS\_OFFSCREENPLAIN に使用できる形式を列挙します。 2番目のメソッドでは、 [**dd\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体に含まれる[**DDCORECAPS**](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造体の**dwnum4 ccコード**メンバーと、dd\_HALINFO 構造体にも含まれる**lpdwFourCC**配列を使用します。

DXT 形式は主にテクスチャとして使用することを目的としているため、ドライバーは、最初のメソッドを使用して DXT 形式のみを列挙します。 DXT 形式を**lpdwFourCC**配列に追加する必要はありません。

 

 





