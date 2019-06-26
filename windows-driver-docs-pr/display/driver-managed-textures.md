---
title: ドライバー管理対象テクスチャ
description: ドライバー管理対象テクスチャ
ms.assetid: 7ec56b86-dc29-41c3-91f4-2a30e9116b61
keywords:
- テクスチャ管理 WDK Direct3D、ドライバー管理
- WDK Direct3D テクスチャのドライバー管理
- 管理可能なテクスチャ WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14ddb04034e4a6d233535c685188b7e4a7d9f6a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381080"
---
# <a name="driver-managed-textures"></a>ドライバー管理対象テクスチャ


## <span id="ddk_driver_managed_textures_gg"></span><span id="DDK_DRIVER_MANAGED_TEXTURES_GG"></span>


ドライバーは、管理可能としてマークされているテクスチャを管理できます。 これらの DirectDrawSurface オブジェクトが、DDSCAPS2 で管理可能としてマークされている\_TEXTUREMANAGE フラグ、 **dwCaps2**によって参照される、構造体のメンバー **lpSurfMore-&gt;ddCapsEx**. (**lpSurfMore**と**ddCapsEx**のメンバーである、 [ **DD\_画面\_ローカル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)と[ **DD\_画面\_詳細**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)構造体に、それぞれします)。

ドライバーを設定してドライバー管理のテクスチャのサポート、 **dwCaps2**のメンバー、 [ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造体を DDCAPS2\_CANMANAGETEXTURE ビット。 ドライバーでは、この DDCORECAPS 構造を指定します、 **ddCaps**のメンバー、 [ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体。 DD\_HALINFO がによって返される[ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)ドライバーの DirectDraw コンポーネントの初期化に応答します。

ドライバーは「レイジー」方式のビデオまたは非ローカル メモリに必要なサーフェスを作成できます。 つまり、ドライバーは、サーフェスをバックアップする必要があります、ラスタライズするプリミティブを使用して、テクスチャの直前にあるまでのテクスチャを残します。

サーフェスは、主に、優先度の割り当てによって削除する必要があります。 ドライバーに応答する、D3DDP2OP\_SETPRIORITY 操作のコードで、 [ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コマンド ストリーム。 この操作のコードでは、特定の画面の優先順位を設定します。 セカンダリの手段として、ドライバーは、サーフェスを削除するのに最も最近使用 (LRU) スキームを使用する必要があります。 ドライバーは、2 つまたは複数のテクスチャの優先順位は、特定のシナリオで同一たびに、このスキームを使用します。 論理的には、使用されている任意の画面のまったく削除されません。

ドライバーが、管理対象のサーフェスをサポートするかどうかは、ドライバーが表示される特殊な[ *DdDestroySurface* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)ビデオ メモリが紛失モードの切り替えが発生した場合など、ケース内のマネージ サーフェスを呼び出します。 この場合は、DRAWISURF\_無効なフラグが設定され、ドライバーは、単にこの管理対象の画面のビデオ メモリのコピーを削除し、他の構造体の状態は保持します。 それ以外の場合、ドライバーは、通常を実行します。 画面の呼び出しを破棄します。

ドライバーを処理する必要があります[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)と[ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)テクスチャを管理するときに適切に呼び出します。 これは、ため、テクスチャをもう一度使用する前に、画面のビデオ メモリ コピーにバッキング画面イメージへの変更を反映する必要があります。 サーフェス、またはそのすべての部分だけを更新する方が適切であるドライバーが決定する必要があります。 などの場合、ドライバーの*DdLock* 、サーフェイスのビデオ メモリのコピーのバックアップ (システム メモリ) のイメージの一部だけを変更する関数が呼び出されますその後、ドライバーの*DdBlt*関数が呼び出される、ドライバーは、必要なビデオ メモリをシステム メモリから表面下だけの中で、更新プログラムを最適化できます。

ドライバーが、テクスチャの最適化の変換を実行するために、またはそれ自体の場所とタイミングを決定する、テクスチャの管理を実行できるメモリのテクスチャを転送します。

 

 





