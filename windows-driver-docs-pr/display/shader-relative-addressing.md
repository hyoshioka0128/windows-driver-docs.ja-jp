---
title: シェーダーの相対アドレス指定
description: シェーダーの相対アドレス指定
ms.assetid: 7f936b56-cd41-4df5-8fc0-b8a7332ca7fa
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d8698434203df69da81c03cb7ff60cef342cb9ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829457"
---
# <a name="shader-relative-addressing"></a>シェーダーの相対アドレス指定


## <span id="ddk_shader_relative_addressing_gg"></span><span id="DDK_SHADER_RELATIVE_ADDRESSING_GG"></span>


相対アドレス指定をサポートするピクセルシェーダーおよび頂点シェーダーのバージョンでは、[ターゲット](destination-parameter-token.md)と[ソースのパラメータートークン](source-parameter-token.md)のビット13で相対アドレスを使用するように指定できます。 相対アドレス指定が指定されている場合、追加の DWORD トークンは、送信先またはソースパラメータートークンの後に続きます。

この相対アドレス指定トークンは、頂点シェーダーバージョン 2\_0 以降およびピクセルシェーダーバージョン 3\_0 以降にのみ存在することに注意してください。 相対アドレス指定は、3\_0 より前のピクセルシェーダーバージョンでは使用されません。

この相対アドレス指定トークンは、送信先またはソースパラメータートークンと同じ形式で、次の規則が適用されます。

-   [レジスタ型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)として使用できるのは、D3DSPR\_ADDR または D3DSPR\_LOOP だけです。

-   ソースパラメータートークンの Swizzle ビットは、レジスタコンポーネントを決定するために使用されます。

-   ビット31は0x1 です。

-   レジスタオフセットが使用されます。

-   その他のビットは使用されません。

アドレスレジスタと aL レジスタは、定数レジスタの相対アドレス指定に使用されます。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

 

 





