---
title: D3DDP2OP_CLEAR DP2 トークンの処理
description: D3DDP2OP_CLEAR DP2 トークンの処理
ms.assetid: ec027f44-bdd5-4d5a-8c47-1ac6a0c1cb6e
keywords:
- DirectX 8.0 リリース ノート WDK Windows 2000 を表示する純粋なデバイスは、D3DDP2OP_CLEAR DP2 トークンの処理
- 純粋なデバイス WDK DirectX 8.0、D3DDP2OP_CLEAR DP2 トークンの処理
- D3DDP2OP_CLEAR WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d68491ef2629189b30c3eb08f641aac01cf6d072
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363706"
---
# <a name="processing-the-d3ddp2opclear-dp2-token"></a>処理、D3DDP2OP\_クリア DP2 トークン


## <span id="ddk_processing_the_d3ddp2op_clear_dp2_token_gg"></span><span id="DDK_PROCESSING_THE_D3DDP2OP_CLEAR_DP2_TOKEN_GG"></span>


DirectX 8.0、D3DDP2OP の必要な処理をいくつかの変更が導入されて\_トークンのクリアします。 新しいフラグ D3DCLEAR 具体的には\_COMPUTERECTS に追加されて、 **dwFlags**のフィールド、 [ **D3DHAL\_DP2CLEAR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2clear)データ構造体。 純粋なデバイスの種類を使用している場合に、この新しいフラグは、ドライバーに渡されるのみ (つまり D3DCREATE\_PUREDEVICE が、D3DDEVCAPS をエクスポートして、デバイスとドライバーを作成するときに指定された\_PUREDEVICE デバイスの上限)。 さらに、DirectX 8.0 ドライバーにはこのフラグが渡されないと、レガシを使用して指定されていない**クリア**または**Clear2**ドライバー コールバック。

 

 





