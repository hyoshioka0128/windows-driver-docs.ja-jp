---
title: シェーダーの相対アドレス指定
description: シェーダーの相対アドレス指定
ms.assetid: 7f936b56-cd41-4df5-8fc0-b8a7332ca7fa
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 134113bdee84951635888abacdef89bb7a670d03
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365507"
---
# <a name="shader-relative-addressing"></a>シェーダーの相対アドレス指定


## <span id="ddk_shader_relative_addressing_gg"></span><span id="DDK_SHADER_RELATIVE_ADDRESSING_GG"></span>


ビット 13 でピクセルと頂点シェーダーのバージョンがサポートの相対アドレスを指定できることその相対アドレス指定が使用される[先](destination-parameter-token.md)と[パラメーター トークンをソース](source-parameter-token.md)します。 相対アドレスを指定すると、追加の DWORD トークンは、移行先またはソース パラメーターのトークンに従います。

この相対アドレス指定のトークンは、頂点シェーダーのバージョン 2 に対してのみ存在することに注意してください。\_0 と以降とピクセル シェーダーのバージョン 3 の\_0 およびそれ以降。 相対アドレス指定に使用されないピクセル シェーダーのバージョン 3 よりも前\_0。

この相対アドレス指定のトークンの形式が変換先と同じまたはソース パラメーター トークンと、次の規則が適用されます。

-   D3DSPR のみ\_ADDR または D3DSPR\_としてループを使用できる[型登録](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)します。

-   ソース パラメーター トークンのスィズル ビットを使用して、登録するコンポーネントを決定します。

-   31 ビットには 0x1 です。

-   レジスタのオフセットが使用されます。

-   その他のすべての bits は使用されません。

アドレス レジスタと aL レジスタは、定数レジスタの相対アドレスを指定するために使用されます。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





