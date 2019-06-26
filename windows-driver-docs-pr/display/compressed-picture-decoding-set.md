---
title: 圧縮画像のデコード セット
description: 圧縮画像のデコード セット
ms.assetid: 7d6e2050-663e-4370-a210-1d319cfbde6d
keywords:
- 圧縮の画像セット WDK DirectX VA のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be96689f3a57cbb29ff8045df2e572ef7a3f3be4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370651"
---
# <a name="compressed-picture-decoding-set"></a>圧縮画像のデコード セット


## <span id="ddk_compressed_picture_decoding_set_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_SET_GG"></span>


このセクションでは、圧縮された画像をデコードの最小限の相互運用性の設定を定義します。 、デコーダーによってこの一連の構成をサポートする必要があり、アクセラレータでこのセット内の 1 つ以上の構成をサポートする必要があります。 [追加の構成セット](additional-encouraged-configuration-set.md)をサポートするには推奨に提供されます (これらの構成は必要ありません)。

このセット内の最初の 6 つの構成は、すべての[制限プロファイル](restricted-profiles.md)します。 このセットの 7 番目の構成が MPEG2 に対してのみ定義されている\_C および MPEG2\_D.

3 番目最後のメンバーからによって圧縮された画像をデコードの構成の最小限の相互運用性の構成セットが定義されている、 [ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)構造体。

 

 





