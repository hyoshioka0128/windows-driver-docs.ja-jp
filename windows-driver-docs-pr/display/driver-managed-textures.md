---
title: ドライバー管理対象テクスチャ
description: ドライバー管理対象テクスチャ
ms.assetid: 7ec56b86-dc29-41c3-91f4-2a30e9116b61
keywords:
- テクスチャ管理 WDK Direct3D、ドライバーで管理
- ドライバーで管理されているテクスチャ WDK Direct3D
- 管理可能なテクスチャ WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afc88e50312503cfb737982bf9127f642f210a1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839729"
---
# <a name="driver-managed-textures"></a>ドライバー管理対象テクスチャ


## <span id="ddk_driver_managed_textures_gg"></span><span id="DDK_DRIVER_MANAGED_TEXTURES_GG"></span>


ドライバーは、管理可能とマークされているテクスチャを管理できます。 これらの DirectDrawSurface オブジェクトは、 **&gt;LP氏 TEXTUREMANAGE ddCapsEx**によって参照される構造体の**DWCAPS2**メンバーの DDSCAPS2\_フラグを使用して、管理しやすいマークが付けられます。 (**Lpを more**および**ddcapsex**は、 [ **\_ローカル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)および[**dd\_\_サーフェイス**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)のメンバーであり、それぞれの構造体は、それぞれによって\_ます)。

ドライバーは、 [**DDCORECAPS**](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造体の**DWCAPS2**メンバーを DDCAPS2\_CANMANAGETEXTURE ビットに設定することによって、ドライバーによって管理されるテクスチャをサポートします。 このドライバーは、 [**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体の**ddcaps**メンバーでこの DDCORECAPS 構造体を指定します。 HALINFO は、ドライバーの DirectDraw コンポーネントの初期化に応じて[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)によって返されます。\_

これにより、ドライバーはビデオまたは非ローカルメモリ内の必要なサーフェイスを "レイジー" 方式で作成できます。 つまり、ドライバーは、テクスチャを使用するプリミティブをラスタライズする直前に、必要になるまでテクスチャをバッキングサーフェイスに残します。

サーフェイスは主に優先順位の割り当てによって削除する必要があります。 ドライバーは、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コマンドストリームの D3DDP2OP\_setpriority 操作コードに応答します。 この操作コードは、指定されたサーフェイスの優先順位を設定します。 セカンダリメジャーとして、ドライバーは、最も最近使用した (LRU) スキームを使用して、サーフェスを削除する必要があります。 特定のシナリオで2つ以上のテクスチャの優先順位が同じである場合、ドライバーはこのスキームを使用します。 論理的には、使用中のすべてのサーフェイスを削除しないでください。

ドライバーが管理対象サーフェスをサポートしている場合、ドライバーは、モードスイッチが発生したときなど、ビデオメモリが失われた場合に、管理対象サーフェイスに対して特殊な[*DdDestroySurface*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)呼び出しを受け取ることがあります。 この場合、DRAWISURF\_無効なフラグが設定され、ドライバーは単純にこの管理対象サーフェイスのビデオメモリコピーを見つけし、他の構造体をそのまま維持します。 それ以外の場合、ドライバーは通常の破棄画面呼び出しを実行します。

ドライバーは、テクスチャを管理するときに、 [*Ddblt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)と[*ddblt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)の呼び出しを適切に処理する必要があります。 これは、テクスチャが再度使用される前に、バッキングサーフェイスイメージへの変更が表面のビデオメモリコピーに反映される必要があるためです。 ドライバーは、表面の一部またはすべてを更新する方がよいかどうかを判断する必要があります。 たとえば、イメージのビデオメモリコピーのバッキング (システムメモリ) イメージの一部のみを変更するためにドライバーの*Ddlock*関数が呼び出された場合、ドライバーの*ddlock*関数が呼び出されると、ドライバーは、次のようにして更新プログラムを最適化することができます。必要なサブサーフェスをシステムメモリからビデオメモリに blitting します。

このドライバーは、テクスチャの最適化変換を実行するため、またはテクスチャをメモリ内でいつどこに転送するかを決定するために、テクスチャ管理を実行できます。

 

 





