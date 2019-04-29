---
title: KSPROPSETID\_DirectSound3DBuffer
description: KSPROPSETID\_DirectSound3DBuffer
ms.assetid: 38ee775a-9b6c-4803-a024-fecc852d122d
keywords:
- KSPROPSETID_DirectSound3DBuffer
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dedd099be95499d3ea2946c8692724ac6430c9c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332539"
---
# <a name="kspropsetiddirectsound3dbuffer"></a>KSPROPSETID\_DirectSound3DBuffer


## <span id="ddk_kspropsetid_directsound3dbuffer_ks"></span><span id="DDK_KSPROPSETID_DIRECTSOUND3DBUFFER_KS"></span>


`KSPROPSETID_DirectSound3DBuffer`プロパティ セットには実装するために必要なすべてのデバイス固有のプロパティが含まれています、 **IDirectSound3DBuffer**インターフェイス (Microsoft Windows SDK のドキュメントを参照してください)。 このプロパティのセットを使用して、API で指定されている 3D バッファーのプロパティは DirectSound と WDM オーディオ ドライバー間で直接渡されます。 このプロパティのセットがによって処理される、 [ **KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md) 3D バッファーと 3D リスナーのプロパティの両方を処理するノードの。

このセット内のプロパティ項目が KSPROPERTY によって指定された\_DIRECTSOUND3DBUFFER 列挙値。

`KSPROPSETID_DirectSound3DBuffer`プロパティ セットには、次のプロパティが含まれています。

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_ALL**](ksproperty-directsound3dbuffer-all.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES**](ksproperty-directsound3dbuffer-coneangles.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION**](ksproperty-directsound3dbuffer-coneorientation.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME**](ksproperty-directsound3dbuffer-coneoutsidevolume.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MAXDISTANCE**](ksproperty-directsound3dbuffer-maxdistance.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE**](ksproperty-directsound3dbuffer-mindistance.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MODE**](ksproperty-directsound3dbuffer-mode.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置**](ksproperty-directsound3dbuffer-position.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_ベロシティ**](ksproperty-directsound3dbuffer-velocity.md)

 

 





