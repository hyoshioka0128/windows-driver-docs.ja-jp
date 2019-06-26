---
title: オフホスト IDCT
description: オフホスト IDCT
ms.assetid: 31797487-0c4e-4b8c-801e-f545bd60cc6d
keywords:
- マクロ ブロック WDK DirectX va なので、IDCT
- 低レベルの IDCT WDK DirectX VA
- オフホスト IDCT WDK DirectX VA
- 逆コサイン不連続変換 WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564d6af5d6c73f6f84b2dfc73dc1b12cd75cdd29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372790"
---
# <a name="off-host-idct"></a>オフホスト IDCT


## <span id="_off_host_idct"></span><span id="_OFF_HOST_IDCT"></span>


オフホスト IDCT 処理するためのマクロ ブロック逆コサイン不連続変換 (IDCT) 係数のデータの転送が完了するスキャンのインデックスと値の情報のバッファーを使用して定義し、変換式を指定します。 インデックス情報は、(ただし、6 ビット数だけは、8 x 8 変換ブロックを本当に必要な)、16 ビット ワードとして送信されます。 符号付き 16 ビット ワードとして変換係数値の情報が送信されます (8 x 8 変換ブロックの通常のケースに必要な 12 ビットだけと*BPP* 8 です)。

変換係数がいずれかで送信される、 [ **DXVA\_TCoefSingle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_tcoefsingle)構造体、または[ **DXVA\_TCoef4Group**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_tcoef4group)構造体。 場合、 **bConfig4GroupedCoefs**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)構造が 0 で、係数は、DXVAを使用して個別に送信されます\_TCoefSingle 構造体。 場合**bConfig4GroupedCoefs**は 1 です。 係数は、DXVA を使用して 4 つのグループに送信される\_TCoef4Group 構造体。

 

 





