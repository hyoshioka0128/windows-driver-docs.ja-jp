---
title: MIP マップテクスチャのサブレベルの生成
description: MIP マップテクスチャのサブレベルの生成
ms.assetid: fbfb0d1b-468d-4e7f-865e-bdc7d19f5516
keywords:
- MIP マップテクスチャ WDK DirectX 9.0、サブレベルの生成
- 'MIP マップテクスチャのサブレベル: WDK DirectX 9.0'
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a55a6966a81061e7d3fa9448f160571ff4a7238
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838933"
---
# <a name="generating-sublevels-of-mip-map-textures"></a>MIP マップテクスチャのサブレベルの生成


## <span id="ddk_generating_sublevels_of_mip_map_textures_gg"></span><span id="DDK_GENERATING_SUBLEVELS_OF_MIP_MAP_TEXTURES_GG"></span>


ディスプレイドライバーは、 [**DDCORECAPS**](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造体の**DWCAPS2**メンバーの DDCAPS2\_canautogenmipmap ビットを設定することによって、MIP マップテクスチャのサブレベルの自動生成をサポートしていることを示します。 このドライバーは、 [**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体の**ddcaps**メンバーでこの DDCORECAPS 構造体を指定します。 DD\_HALINFO は、ドライバーの[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)関数によって返されます。 また、表示ドライバーは、特定のサーフェイス形式が、 [**Ddのピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)の**dwoperations**メンバーで D3DFORMAT\_OP\_autogenmipmap フラグを設定して、サブレベルの自動生成をサポートしているかどうかも示します。形式の構造体。

テクスチャサーフェイスが作成されると、Direct3D ランタイムは、このテクスチャの MIP マップのサブレベルが自動的に使用されることを示すために、DDSCAPSEX ([**DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))) 構造体の**DWCAPS3**メンバーの DDSCAPS3\_autogenmipmap ビットを設定します。れる. Direct3D が mipmap マップのサブレベルを自動的に生成するようにテクスチャを設定し、一部のテクスチャが自動的に生成されないようにする場合、ドライバーは次に示すように、これらのテクスチャに対して array.blit 操作 (D3DDP2OP\_TEXBLT) のみを実行できます。モデル

-   ドライバーは、MIP マップを自動的に生成するソーステクスチャからは array.blit ません。

-   Mipmap が自動生成されないソーステクスチャから blits ドライバーが、そのテクスチャに対して自動的に生成しない場合、ドライバーは最上位の一致レベルのみを blits します。 ソーステクスチャからのサブレベルは無視されます。 ターゲットのサブレベルを生成できます。

-   同様に、ドライバーが、MIP マップを自動生成するためにソースと宛先のテクスチャから blits した場合、ドライバーは最上位の一致レベルのみを blits します。 ソーステクスチャからのサブレベルは無視されます。 ターゲットのサブレベルを生成できます。

MIP マップテクスチャのサブレベルを生成するために、ドライバーは[**D3DHAL\_DP2GENERATEMIPSUBLEVELS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2generatemipsublevels)構造と共に D3DDP2OP\_GENERATEMIPSUBLEVELS コマンドを受け取ります。 このコマンドを受け取るには、テクスチャのサーフェイス形式で、D3DFORMAT\_OP\_AUTOGENMIPMAP フラグを公開する必要があります。

ドライバーで管理された[リソース](driver-managed-resources.md)の場合、ドライバーがビデオメモリ内のリソースを見つけして置き換えるときに、ドライバーは最後に設定されたフィルターの種類を使用して、サブレベルを自動的に生成する必要があります。 Direct3D はリソースの削除と交換を制御しないため、Direct3D は D3DDP2OP\_GENERATEMIPSUBLEVELS コマンドをドライバーに送信しません。

Direct3D ランタイムは、ドライバーの[*Ddlock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)関数を呼び出すことができません。また、他の[DDI](direct3d-driver-ddi.md)を使用して、自動生成された mipmap マップテクスチャのサブレベルにアクセスすることもできません。 これは、軽量の MIP マップテクスチャのように自動生成された mipmap マップテクスチャのサブレベルが "暗黙的" であり、ドライバーで必要に応じて指定できることを意味します。 このドライバーでは、"complete" surface データ構造を指定する必要はありません。 ただし、Direct3D は、ドライバーの*Ddlock*または[*ddlock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)関数を呼び出したり、D3DDP2OP\_BLT コマンドを送信したり、他の DDI を使用したりできる必要があることに注意してください ([ドライバーで管理](driver-managed-textures.md)されているテクスチャ、動的テクスチャ、またはベンダー固有の形式の場合のみ)。自動生成された mipmap マップテクスチャの最上位レベルにアクセスする場合は。

 

 





