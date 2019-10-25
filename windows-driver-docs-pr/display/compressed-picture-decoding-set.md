---
title: 圧縮画像のデコード セット
description: 圧縮画像のデコード セット
ms.assetid: 7d6e2050-663e-4370-a210-1d319cfbde6d
keywords:
- 圧縮された画像デコードセット WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98d7722f4ab076d24f86a239dd95e2222012dc31
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839798"
---
# <a name="compressed-picture-decoding-set"></a>圧縮画像のデコード セット


## <span id="ddk_compressed_picture_decoding_set_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_SET_GG"></span>


このセクションでは、圧縮画像デコード用の最小相互運用性構成セットを定義します。 この一連の構成はデコーダーによってサポートされる必要があり、このセットの1つ以上の構成がアクセラレータによってサポートされている必要があります。 サポートを推奨する[追加の構成セット](additional-encouraged-configuration-set.md)が用意されています (これらの構成は必要ありません)。

このセットの最初の6つの構成は、制限されたすべての[プロファイル](restricted-profiles.md)を対象としています。 このセットの7番目の構成は、MPEG2\_C と MPEG2\_D に対してのみ定義されています。

圧縮された画像デコード用の構成の最小相互運用性構成セットは、3番目と[**DXVA\_configpicture デコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の最後のメンバーによって定義されます。

 

 





