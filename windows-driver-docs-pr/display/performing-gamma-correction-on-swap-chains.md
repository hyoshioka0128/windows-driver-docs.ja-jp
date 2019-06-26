---
title: スワップ チェーンに対するガンマ補正の実行
description: スワップ チェーンに対するガンマ補正の実行
ms.assetid: 4912cd15-bd56-43b6-9419-66917bf3f72c
keywords:
- ガンマ補正 WDK DirectX 9.0、スワップ チェーン
- スワップ チェーン WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4708fa23b6faeb5a2c0d68115d026eaa4f39e0b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385571"
---
# <a name="performing-gamma-correction-on-swap-chains"></a>スワップ チェーンに対するガンマ補正の実行


## <span id="ddk_performing_gamma_correction_on_swap_chains_gg"></span><span id="DDK_PERFORMING_GAMMA_CORRECTION_ON_SWAP_CHAINS_GG"></span>


アプリケーションでは、正しく描画操作を実行するには、線形のカラー領域で、スワップ チェーンのバック バッファーを維持できます。 デスクトップが通常でないため線形のカラー スペース、デスクトップの内容を表示する前にバック バッファーの内容にガンマ補正が必要です。

アプリケーションを呼び出す、 **IDirect3DSwapChain9::Present**スワップ チェーンで次のバック バッファーの内容を表示するメソッド。 この呼び出しで、バック バッファーの内容が線形のカラー スペースのことを示す、アプリケーション設定、D3DPRESENT\_線形\_コンテンツのフラグ。 DirectX 9.0、ランタイムは、ディスプレイ ドライバーを呼び出す[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 、DDBLT で関数を\_拡張\_フラグと DDBLT\_拡張\_線形\_コンテンツ フラグを設定します。 ドライバーがこれを受信するときに*DdBlt*ソース画面に線形のカラー スペース内のコンテンツが含まれている呼び出し、ドライバーを決定します。 ドライバーは、blt の一部として線形のカラー スペースを 2.2 のガンマ補正 (sRGB) を実行できます。 拡張 blit フラグの詳細については、次を参照してください。[拡張 Blt フラグ](extended-blt-flags.md)します。

ドライバーの設定、D3DCAPS3\_線形\_TO\_SRGB\_のプレゼンテーション機能ビット、 **Caps3**をそのデバイスがガンマ値 2.2 をサポートしていることを示す D3DCAPS9 構造体のメンバー修正します。 ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 」の説明に従って D3DCAPS8 構造体を返すにする方法と同様にクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

詳細については**IDirect3DSwapChain*Xxx*:: 存在する**、DirectX SDK の最新のドキュメントを参照してください。

 

 





