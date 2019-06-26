---
title: 軽量の MIP マップ テクスチャの処理
description: 軽量の MIP マップ テクスチャの処理
ms.assetid: f541b046-2937-428c-ab98-eb1020728e04
keywords:
- MIP マップ テクスチャ WDK DirectX 9.0、軽量
- 軽量の MIP マップ テクスチャ WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce1f698c80014aaa56c4ea4a212569d8ae8bf2d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372938"
---
# <a name="handling-lightweight-mip-map-textures"></a>軽量の MIP マップ テクスチャの処理


## <span id="ddk_handling_lightweight_mip_map_textures_gg"></span><span id="DDK_HANDLING_LIGHTWEIGHT_MIP_MAP_TEXTURES_GG"></span>


軽量の MIP マップ テクスチャの MIP 下位レベルが暗黙的に指定し、DirectDraw surface の対応する構造がないため ([**DD\_画面\_ローカル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)、 [**DD\_画面\_GLOBAL** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)と[ **DD\_画面\_詳細**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more))、DirectX 9.0 バージョンのドライバーには、MIP マップ テクスチャは軽量で、メモリを節約する不要なドライバーの表面構造が作成されないようにする場合を判断できます。 場合、ドライバーが確認の MIP マップ テクスチャが軽量の場合を決定する、DDSCAPS3\_LIGHTWEIGHTMIPMAP ビット、 **dwCaps3** 、DDSCAPSEX のメンバー ([**DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85)))テクスチャのサーフェイスでの構造を設定します。

すべての MIP マップ テクスチャ DirectX 9.0 では既定では軽量ことに注意してください。

DirectX 9.0 バージョンのドライバーでは軽量で、重い紙の MIP マップ テクスチャを処理するときに、次の規則を監視します。

-   DirectX 9.0 と以降のドライバーが、D3DDP2OP を受信できる\_TEXBLT 操作コードのソースの MIP マップ テクスチャの重量と転送先の MIP マップ テクスチャは lightweight またはその逆です。 もちろん、ドライバーを受け取ることも、D3DDP2OP\_TEXBLT MIP マップ テクスチャをソースと宛先の両方の軽量です。

-   システム メモリに軽量の MIP マップ テクスチャは、メモリの 1 つの画面のみを消費するので、全体の MIP マップは最上位レベルの画面内でドライバーに表示されます。 ドライバーは、システム メモリに軽量の MIP マップ テクスチャから直接、テクスチャの操作を実行する必要はありません。 このような MIP マップ テクスチャが、D3DDP2OP のソースにできるだけ\_TEXBLT します。

-   ロックと直接のビデオに書き込まれるために、次の MIP マップ テクスチャは重量をする必要がありますまたは[AGP](agp-support.md)各サブレベルに対応するメモリがこのようなテクスチャでできること。

    -   レンダー ターゲット
    -   深度ステンシル
    -   動的
    -   書式設定された仕入先

    したがって、サーフェスの完全なデータ構造は、サブレベルにつきが必要です。

-   ビデオまたは AGP メモリ軽量の MIP マップ テクスチャが決してロックされているかなどの他の Ddi によって参照される[ *DdBlt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)ドライバーは、このような MIP マップ テクスチャのサブレベルの配置を決定します。 そのため、完全なサーフェス (明示的な**fpVidmem**のメンバー、 [ **DD\_画面\_グローバル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)構造) などのサブレベルのMIP マップ テクスチャは必要ありません。

-   軽量の MIP マップ テクスチャのドライバー管理は、1 つの画面にも制限され、Direct3D がシステム メモリの軽量の MIP マップ テクスチャを使用している同じレイアウトだけを使用する必要があります。 これがありません (実装のコスト) を除く悪影響を与えるのため、対応する常駐 (ビデオおよび AGP) の MIP マップ テクスチャは、独自の実装に固有のレイアウトを持つことができます。

 

 





