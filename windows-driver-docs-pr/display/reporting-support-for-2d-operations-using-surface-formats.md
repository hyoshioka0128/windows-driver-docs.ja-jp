---
title: サーフェスの形式を使用した 2D 操作に対するサポートのレポート
description: サーフェスの形式を使用した 2D 操作に対するサポートのレポート
ms.assetid: c7737daf-3342-48dc-a365-f789b7203013
keywords:
- 2次元操作 (WDK DirectX 9.0、surface 形式)
- 2D 操作 WDK DirectX 9.0、surface 形式
- surface 形式 WDK DirectX 9.0
- surface 形式 WDK DirectX 9.0、2D 操作のレポートサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1728a140c98029b8e3d12a8de9e2b0353dee2e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829595"
---
# <a name="reporting-support-for-2d-operations-using-surface-formats"></a>サーフェスの形式を使用した 2D 操作に対するサポートのレポート


## <span id="ddk_reporting_support_for_2d_operations_using_surface_formats_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_2D_OPERATIONS_USING_SURFACE_FORMATS_GG"></span>


ドライバーは、その形式を使用して2D 操作を実行できることを示すために、 [**ddの形式の Ddピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)構造の**dwoperations**メンバーのフラグを指定します。

たとえば、ドライバーは、D3DFORMAT\_OP\_OFFSCREENPLAIN フラグを設定することによって、画面の間でコピーや塗りつぶしを行うことができることを示すことができます。

ドライバーがベンダーから提供されたコードまたは D3DFORMAT 列挙型のコードを使用して、 **Ddfourcc 形式の dwfourcc**メンバーを設定し、surface の形式を割り当てる場合、ドライバーは D3DFORMAT\_OP\_使用して\_をに変換することもでき @no__t(4_ ARGB および D3DFORMAT\_MEMBEROFGROUP\_、ソースとターゲットの両方のサーフェス間でカラー変換を実行できるかどうかを示すための ARGB フラグです。 つまり、D3DFORMAT\_MEMBEROFGROUP\_ARGB フラグが設定されているターゲットサーフェイスは、D3DFORMAT\_\_OP を持つ任意のソースサーフェイスから、\_を\_ARGB フラグセットに変換するために、その色の形式を変換できることを示します。

ドライバーで指定できるのは、チャネルごとに少なくとも5ビットの色情報が含まれているターゲットサーフェス形式に対して、D3DFORMAT\_MEMBEROFGROUP\_ARGB フラグのみです。 つまり、DDピクセル形式の**Dwfourcc**メンバーで設定されている D3DFMT\_A1R5G5B5 形式が有効です。 ただし、D3DFMT\_A4R4G4B4 形式は無効です。 また、D3DFORMAT\_OP\_指定すると、ドライバーは特定のソースサーフェイス形式に制限され、\_を\_ARGB フラグに変換できます。 ソース形式は、D3DFORMAT\_MEMBEROFGROUP\_ARGB フラグまたは*FOURCC*の表面形式に対して有効な任意の形式にすることができます。

D3DFORMAT\_OP\_\_を\_ARGB および D3DFORMAT\_MEMBEROFGROUP に変換することはできますが、argb 形式が使用されていることに注意してください。このランタイムでは、XRGB 形式のサーフェイスを指定することもできます (たとえば、、D3DFMT\_X1R5G5B5)。 ドライバーで D3DFORMAT\_MEMBEROFGROUP\_ARGB または D3DFORMAT\_OP\_指定した場合、\_を無効な形式で\_に変換すると、ランタイムによって Direct3D HAL が読み込まれなくなります。

 

 





