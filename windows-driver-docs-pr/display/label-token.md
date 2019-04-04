---
title: トークンにラベルを付ける
description: トークンにラベルを付ける
ms.assetid: 29b2b4b1-c599-4bea-9d83-3a10eedac4a6
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: bae11eb53c3de8110e1068cc9c5bcac5e95be8f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530766"
---
# <a name="label-token"></a>トークンにラベルを付ける


## <span id="ddk_label_token_gg"></span><span id="DDK_LABEL_TOKEN_GG"></span>


ラベル トークンは特定の操作にのみ使用されます (たとえば、D3DSIO\_CALLNZ) と次のビットで構成されます。

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_10_00_"></span>**\[10時 00分\]** 0 ~ 10 のビットがレジスタ番号 (登録ファイル内のオフセット) を示します。

<span id="_12_11_"></span>**\[12時 11分\]** ビット 11 と 12 は、4 番目と 5 番目のビット\[3, 4\]を示すため、[の種類を登録](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

<span id="_27_13_"></span>**\[27:13\]** ピクセル シェーダー (PS) と頂点シェーダー (VS) のすべてのバージョン用に予約されています。 この値は、「0x0」に設定されます。

<span id="_30_28_"></span>**\[30:28\]**  30 からビット 28 は最初の 3 つのビット\[0,1,2\]を示すため、[の種類を登録](https://msdn.microsoft.com/library/windows/hardware/ff569707)します。

<span id="_31_"></span>**\[31\]** ビット 31 は 0x1 です。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ラベルのトークンの形式と同じ、[ソース パラメーター トークン](source-parameter-token.md)レジスタ数と種類フィールドのみが使用される点が異なります。

ビット 28、29、30、11、および 12 フォーム register 型を示す 5 ビット値です。 登録の種類については、[シェーダー登録型](https://msdn.microsoft.com/library/windows/hardware/ff569707)を参照してください。 D3DSPR としてラベル トークンを register 型を指定する必要があります\_ラベル。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





