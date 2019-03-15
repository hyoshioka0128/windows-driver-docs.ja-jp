---
title: 圧縮する画像のセットをデコード
description: 圧縮する画像のセットをデコード
ms.assetid: 7d6e2050-663e-4370-a210-1d319cfbde6d
keywords:
- 圧縮の画像セット WDK DirectX VA のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d556a2cb35dd002155f0d74dbbce0f90d04c322e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529634"
---
# <a name="compressed-picture-decoding-set"></a>圧縮する画像のセットをデコード


## <span id="ddk_compressed_picture_decoding_set_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_SET_GG"></span>


このセクションでは、圧縮された画像をデコードの最小限の相互運用性の設定を定義します。 、デコーダーによってこの一連の構成をサポートする必要があり、アクセラレータでこのセット内の 1 つ以上の構成をサポートする必要があります。 [追加の構成セット](additional-encouraged-configuration-set.md)をサポートするには推奨に提供されます (これらの構成は必要ありません)。

このセット内の最初の 6 つの構成は、すべての[制限プロファイル](restricted-profiles.md)します。 このセットの 7 番目の構成が MPEG2 に対してのみ定義されている\_C および MPEG2\_D.

3 番目最後のメンバーからによって圧縮された画像をデコードの構成の最小限の相互運用性の構成セットが定義されている、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体。

 

 




