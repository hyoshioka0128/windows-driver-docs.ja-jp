---
title: ラベル トークン
description: ラベル トークン
ms.assetid: 29b2b4b1-c599-4bea-9d83-3a10eedac4a6
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ea3fee6110e0675684752f7f5de4b38e36524723
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840332"
---
# <a name="label-token"></a>ラベル トークン


## <span id="ddk_label_token_gg"></span><span id="DDK_LABEL_TOKEN_GG"></span>


ラベルトークンは、特定の操作 (D3DSIO\_CALLNZ など) にのみ使用され、次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>列

<span id="_10_00_"></span> **\[10:00\]** ビット 0 ~ 10 はレジスタ番号 (レジスタファイル内のオフセット) を示します。

<span id="_12_11_"></span> **\[12:11\]** ビット11と12は、4番目と5番目の \[3, 4\][レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を示すために使用します。

<span id="_27_13_"></span> **\[27:13\]** すべてのバージョンのピクセルシェーダー (PS) と頂点シェーダー (VS) 用に予約されています。 この値は0x0 に設定されます。

<span id="_30_28_"></span> **\[30:28\]** ビット 28 ~ 30 は、[レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を示すために0、1、2\] \[最初の3ビットです。

<span id="_31_"></span> **\[31\]** ビット31は0x1 です。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

ラベルトークンの形式は、レジスタの数値と型のフィールドのみが使用される点を除いて、[ソースパラメーターのトークン](source-parameter-token.md)と同じです。

ビット28、29、30、11、および12は、レジスタの種類を示す5ビットの値です。 レジスタ型の詳細については、「[シェーダーレジスタ型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)」を参照してください。 ラベルトークンのレジスタ型は、D3DSPR\_LABEL として指定する必要があります。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

 

 





