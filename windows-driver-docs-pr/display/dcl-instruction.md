---
title: DCL 命令形式
description: DCL 命令形式
ms.assetid: 2833fe6a-f430-4a34-936f-04e997063671
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0117a883bd9ac1a8bd1090b368768fdfa1d56ff4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358671"
---
# <a name="dcl-instruction-format"></a>DCL 命令形式


## <span id="ddk_dcl_instruction_gg"></span><span id="DDK_DCL_INSTRUCTION_GG"></span>


DCL 命令は、レジスタを宣言します。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>書式設定

**ピクセル シェーダー 2\_0 と以降のみです。**

**サンプラーの状態でのみ登録します。**

[命令のトークン](instruction-token.md)

D3DSIO を含む\_DCL します。
DWORD トークン

次のビットの形式があります。

**\[26:0\]** 予約します。 0x0 に設定します。

**\[30:27\]**  D3DSAMPLER に設定\_テクスチャ\_2D、cube、およびなどの型。

**\[31\]**  0x1 に設定します。

[変換先のパラメーターのトークン](destination-parameter-token.md)

登録数を示す、[の種類を登録](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)D3DSPR として\_サンプラーします。 これらは、このトークンで使用されているフィールドのみです。

**入力またはテクスチャのみを登録します。**

[命令のトークン](instruction-token.md)

D3DSIO を含む\_DCL します。
DWORD トークン

次のビットの形式があります。

**\[30:0\]** 予約します。 0x0 に設定します。

**\[31\]**  0x1 に設定します。

[変換先のパラメーターのトークン](destination-parameter-token.md)

入力またはテクスチャのレジスタ番号を示します。 書き込みマスク フィールドでは、宣言されたコンポーネントを示します。

**頂点シェーダー 2\_0 と以降のみです。**

**入力レジスタのみです。**

[命令のトークン](instruction-token.md)

D3DSIO を含む\_DCL します。
DWORD トークン

次のビットの形式があります。

**\[4:0\]**  D3DDECLUSAGE 値 (つまり、D3DDECLUSAGE\_テクスチャ座標、D3DDECLUSAGE\_NORMAL、という具合)。

**\[15:5\]** 予約します。 0x0 に設定します。

**\[19時 16分\]** 使用法のインデックス値。

**\[30:20\]** 予約します。 0x0 に設定します。

**\[31\]**  0x1 に設定します。

[変換先のパラメーターのトークン](destination-parameter-token.md)

登録数を示す、[の種類を登録](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)D3DSPR として\_入力します。 書き込みマスク フィールドでは、宣言されたコンポーネントを示します。

**ピクセル シェーダー 3\_0 と以降のみです。**

**テクスチャ レジスタのみです。**

[命令のトークン](instruction-token.md)

D3DSIO を含む\_DCL します。
DWORD トークン

次のビットの形式があります。

**\[4:0\]**  D3DDECLUSAGE 値 (D3DDECLUSAGE 必要があります\_テクスチャ座標または D3DDECLUSAGE\_色)。

**\[15:5\]** 予約します。 0x0 に設定します。

**\[19時 16分\]** 使用法のインデックス値。 D3DDECLUSAGE の\_、テクスチャ座標は 0 ~ 7 である必要があります。 D3DDECLUSAGE の\_色、0 にする必要があります。

**\[30:20\]** 予約します。 0x0 に設定します。

**\[31\]**  0x1 に設定します。

[変換先のパラメーターのトークン](destination-parameter-token.md)

登録数を示す、[の種類を登録](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)D3DSPR として\_テクスチャ。 書き込みマスク フィールドでは、宣言されたコンポーネントを示します。

**顔がのみに登録します。**

[命令のトークン](instruction-token.md)

D3DSIO を含む\_DCL します。
DWORD トークン

次のビットの形式があります。

**\[30:0\]** 予約します。 0x0 に設定します。

**\[31\]**  0x1 に設定します。

[変換先のパラメーターのトークン](destination-parameter-token.md)

顔のレジスタを示します。 使用されませんが、書き込みマスク フィールドにいっぱいになる必要があります。 結果修飾子キーと shift キーを押しスケール フィールドは 0 (も使用されていない) である必要があります。

**位置でのみ登録します。**

[命令のトークン](instruction-token.md)

D3DSIO を含む\_DCL します。
DWORD トークン

次のビットの形式があります。

**\[30:0\]** 予約します。 0x0 に設定します。

**\[31\]**  0x1 に設定します。

[変換先のパラメーターのトークン](destination-parameter-token.md)

位置のレジスタを示します。 書き込みマスク フィールドでは、宣言されたコンポーネントを示します。

**頂点シェーダー 3\_0 と以降のみです。**

**出力でのみ登録します。**

[命令のトークン](instruction-token.md)

D3DSIO を含む\_DCL します。
DWORD トークン

次のビットの形式があります。

**\[4:0\]**  D3DDECLUSAGE 値 (つまり、D3DDECLUSAGE\_テクスチャ座標、D3DDECLUSAGE\_NORMAL、という具合)。

**\[15:5\]** 予約します。 0x0 に設定します。

**\[19時 16分\]** 使用法のインデックス値。

**\[30:20\]** 予約します。 0x0 に設定します。

**\[31\]**  0x1 に設定します。

[変換先のパラメーターのトークン](destination-parameter-token.md)

登録数を示す、[の種類を登録](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)D3DSPR として\_出力します。 コンポーネントが記述された書き込みマスク フィールドを定義します。

いくつか DCL 手順では、出力を記述するには、同じレジスタのオフセットを使用できることに注意してください。 ただし、各 DCL 命令の書き込みマスク コンポーネントは、さまざまなである必要があります。 たとえば、次は頂点シェーダー 3 では有効で\_0 以降。

```registry
       DCL   o10.xy
       DCL   o10.zw
```

出力 DCL 手順については、頂点シェーダー 3 で作成したすべてのレジスタを宣言する必要があります\_0 およびそれ以降。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





