---
title: D3DDP2OP_CLEAR DP2 トークンの処理
description: D3DDP2OP_CLEAR DP2 トークンの処理
ms.assetid: ec027f44-bdd5-4d5a-8c47-1ac6a0c1cb6e
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、pure devices、D3DDP2OP_CLEAR DP2 token processing
- ピュアデバイス WDK DirectX 8.0、D3DDP2OP_CLEAR DP2 token processing
- D3DDP2OP_CLEAR WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a200a85af8b712b72fa40eac63a765a67663f18
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829683"
---
# <a name="processing-the-d3ddp2op_clear-dp2-token"></a>D3DDP2OP\_CLEAR DP2 トークンを処理しています


## <span id="ddk_processing_the_d3ddp2op_clear_dp2_token_gg"></span><span id="DDK_PROCESSING_THE_D3DDP2OP_CLEAR_DP2_TOKEN_GG"></span>


DirectX 8.0 では、D3DDP2OP\_CLEAR トークンの必要な処理にいくつかの変更が導入されています。 具体的には、新しいフラグ D3DCLEAR\_COMPUTERECTS が[**D3DHAL\_DP2CLEAR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2clear) data 構造の**dwFlags**フィールドに追加されています。 この新しいフラグは、純粋なデバイスの種類が使用されている場合にのみドライバーに渡されます (つまり、デバイスの作成時に D3DCREATE\_PUREDEVICE が指定され、ドライバーは D3DDEVCAPS\_PUREDEVICE device cap をエクスポートします)。 さらに、このフラグは DirectX 8.0 以外のドライバーに渡されることはなく、従来の**Clear**または**Clear2**ドライバーコールバックを使用して指定されることはありません。

 

 





