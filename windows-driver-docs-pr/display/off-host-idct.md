---
title: オフホスト IDCT
description: オフホスト IDCT
ms.assetid: 31797487-0c4e-4b8c-801e-f545bd60cc6d
keywords:
- マクロが WDK DirectX VA、IDCT をブロックする
- 低レベルの IDCT WDK DirectX VA
- オフホスト IDCT WDK DirectX VA
- 逆余弦変換-WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 749c9e1bc5cf2cf2db7666c8eed630976f9d85f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840505"
---
# <a name="off-host-idct"></a>オフホスト IDCT


## <span id="_off_host_idct"></span><span id="_OFF_HOST_IDCT"></span>


外部ホストの IDCT 処理のために、マクロの逆余弦変換 (IDCT) 係数データの転送は、インデックスと値のスキャンのバッファーを使用して定義し、変換式を指定します。 インデックス情報は16ビットワードとして送信されます (8 ビットの数値のみが8x8 変換ブロックに必要です)。 変換係数の値の情報は、16ビットの符号付きワードとして送信されます (ただし、通常は8x8 変換ブロックと*BPP*が8に等しい場合にのみ必要です)。

変換係数は、 [**DXVA\_TCoefSingle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_tcoefsingle)構造体または[**DXVA\_TCoef4Group**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_tcoef4group)構造体のいずれかで送信されます。 [**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**bConfig4GroupedCoefs**メンバーがゼロの場合、DXVA\_tcoefsingle 構造体を使用して係数が個別に送信されます。 **BConfig4GroupedCoefs**が1の場合、係数は、DXVA\_TCoef4Group 構造体を使用して4つのグループに送信されます。

 

 





