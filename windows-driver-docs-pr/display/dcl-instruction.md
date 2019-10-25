---
title: DCL 命令形式
description: DCL 命令形式
ms.assetid: 2833fe6a-f430-4a34-936f-04e997063671
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ff5fd4c0c19bd26072167c252b4a9f1384a3dccd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839767"
---
# <a name="dcl-instruction-format"></a>DCL 命令形式


## <span id="ddk_dcl_instruction_gg"></span><span id="DDK_DCL_INSTRUCTION_GG"></span>


DCL 命令はレジスタを宣言します。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>形式

**ピクセルシェーダー 2\_0 以降のみ。**

**サンプラー状態レジスタのみ。**

[命令トークン](instruction-token.md)

D3DSIO\_DCL を含みます。
DWORD トークン

のビット形式は次のとおりです。

**\[26:0\]** 確保. を0x0 に設定します。

**\[30:27\]** 2D、キューブなどの\_テクスチャ\_の種類に設定します。

**\[31\]** 0x1 に設定します。

[ターゲットパラメータートークン](destination-parameter-token.md)

レジスタ番号と[レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を D3DSPR\_サンプラーとして示します。 これらは、このトークンで使用される唯一のフィールドです。

**入力またはテクスチャレジスタのみ。**

[命令トークン](instruction-token.md)

D3DSIO\_DCL を含みます。
DWORD トークン

のビット形式は次のとおりです。

**\[30:0\]** 確保. を0x0 に設定します。

**\[31\]** 0x1 に設定します。

[ターゲットパラメータートークン](destination-parameter-token.md)

入力またはテクスチャのレジスタ番号を示します。 [書き込みマスク] フィールドは、宣言されたコンポーネントを示します。

**頂点シェーダー 2\_0 以降のみ。**

**入力レジスタのみ。**

[命令トークン](instruction-token.md)

D3DSIO\_DCL を含みます。
DWORD トークン

のビット形式は次のとおりです。

**\[4:0\]** D3DDECLUSAGE value (つまり、D3DDECLUSAGE\_TEXCOORD、D3DDECLUSAGE\_NORMAL など)。

**\[15:5\]** 確保. を0x0 に設定します。

**\[19:16\]** 使用状況のインデックス値。

**\[30:20\]** 確保. を0x0 に設定します。

**\[31\]** 0x1 に設定します。

[ターゲットパラメータートークン](destination-parameter-token.md)

D3DSPR\_入力として登録番号と[レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を示します。 [書き込みマスク] フィールドは、宣言されたコンポーネントを示します。

**ピクセルシェーダー 3\_0 以降のみ。**

**テクスチャレジスタのみ。**

[命令トークン](instruction-token.md)

D3DSIO\_DCL を含みます。
DWORD トークン

のビット形式は次のとおりです。

**\[4:0\]** D3DDECLUSAGE value (D3DDECLUSAGE\_TEXCOORD または D3DDECLUSAGE\_COLOR) を指定する必要があります。

**\[15:5\]** 確保. を0x0 に設定します。

**\[19:16\]** 使用状況のインデックス値。 D3DDECLUSAGE\_TEXCOORD の場合、は0-7 である必要があります。 D3DDECLUSAGE\_COLOR の場合、は0である必要があります。

**\[30:20\]** 確保. を0x0 に設定します。

**\[31\]** 0x1 に設定します。

[ターゲットパラメータートークン](destination-parameter-token.md)

レジスタ番号と[レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を D3DSPR\_テクスチャとして示します。 [書き込みマスク] フィールドは、宣言されたコンポーネントを示します。

**顔レジスタのみ。**

[命令トークン](instruction-token.md)

D3DSIO\_DCL を含みます。
DWORD トークン

のビット形式は次のとおりです。

**\[30:0\]** 確保. を0x0 に設定します。

**\[31\]** 0x1 に設定します。

[ターゲットパラメータートークン](destination-parameter-token.md)

フェイスレジスタを示します。 書き込みマスクフィールドは未使用であるにもかかわらず、いっぱいになっている必要があります。 結果修飾子とシフトスケールのフィールドは、0 (または未使用) である必要があります。

**位置登録のみです。**

[命令トークン](instruction-token.md)

D3DSIO\_DCL を含みます。
DWORD トークン

のビット形式は次のとおりです。

**\[30:0\]** 確保. を0x0 に設定します。

**\[31\]** 0x1 に設定します。

[ターゲットパラメータートークン](destination-parameter-token.md)

位置レジスタを示します。 [書き込みマスク] フィールドは、宣言されたコンポーネントを示します。

**頂点シェーダー 3\_0 以降のみ。**

**出力レジスタのみ。**

[命令トークン](instruction-token.md)

D3DSIO\_DCL を含みます。
DWORD トークン

のビット形式は次のとおりです。

**\[4:0\]** D3DDECLUSAGE value (つまり、D3DDECLUSAGE\_TEXCOORD、D3DDECLUSAGE\_NORMAL など)。

**\[15:5\]** 確保. を0x0 に設定します。

**\[19:16\]** 使用状況のインデックス値。

**\[30:20\]** 確保. を0x0 に設定します。

**\[31\]** 0x1 に設定します。

[ターゲットパラメータートークン](destination-parameter-token.md)

レジスタ番号と[レジスタの種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)を D3DSPR\_の出力として示します。 書き込みマスクフィールドは、書き込まれるコンポーネントを定義します。

出力を記述するいくつかの DCL 命令は、同じレジスタオフセットを使用できることに注意してください。 ただし、各 DCL 命令の書き込みマスクコンポーネントは異なっている必要があります。 たとえば、次の例は、頂点シェーダー 3\_0 以降で有効です。

```registry
       DCL   o10.xy
       DCL   o10.zw
```

出力の DCL 命令は、頂点シェーダー 3\_0 以降によって書き込まれたすべてのレジスタを宣言する必要があります。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

 

 





