---
title: KSPROPSETID\_DirectSound3DListener
description: KSPROPSETID\_DirectSound3DListener
ms.assetid: 37eef2cb-5b45-4ff8-abb9-a685f0b290e3
keywords:
- KSPROPSETID_DirectSound3DListener
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdea3c9034a9acd8c404e9c8fe2e17fcdca578ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332524"
---
# <a name="kspropsetiddirectsound3dlistener"></a>KSPROPSETID\_DirectSound3DListener


## <span id="ddk_kspropsetid_directsound3dlistener_ks"></span><span id="DDK_KSPROPSETID_DIRECTSOUND3DLISTENER_KS"></span>


`KSPROPSETID_DirectSound3DListener`プロパティ セットには実装するために必要なすべてのデバイス固有のプロパティが含まれています、 **IDirectSound3DListener**インターフェイス (Microsoft Windows SDK のドキュメントを参照してください)。 このプロパティのセットを使用して、API で指定されている 3D バッファーのプロパティは DirectSound と WDM オーディオ ドライバー間で直接渡されます。 このプロパティのセットがによって処理される、 [ **KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)ノード。 WDM オーディオ ドライバーは、同一のリスナーを共有する他のバッファーに、更新されたリスナーのプロパティを適用する必要がありますので、このノードは両方、3D バッファーおよび 3D リスナーのプロパティを処理します。

このセット内のプロパティ項目が KSPROPERTY によって指定された\_DIRECTSOUND3DLISTENER 列挙値。

`KSPROPSETID_DirectSound3DListener`プロパティ セットには、次のプロパティが含まれています。

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ALL**](ksproperty-directsound3dlistener-all.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ALLOCATION**](ksproperty-directsound3dlistener-allocation.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_バッチ**](ksproperty-directsound3dlistener-batch.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_意味**](ksproperty-directsound3dlistener-dopplerfactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_向き**](ksproperty-directsound3dlistener-orientation.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_位置**](ksproperty-directsound3dlistener-position.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR**](ksproperty-directsound3dlistener-rollofffactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ベロシティ**](ksproperty-directsound3dlistener-velocity.md)

 

 





