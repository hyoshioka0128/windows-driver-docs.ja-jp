---
title: KSNODETYPE\_3D\_効果
description: KSNODETYPE\_3D\_効果
ms.assetid: 8b19423b-c1ad-4b59-bdae-a53bb99469ea
keywords:
- KSNODETYPE_3D_EFFECTS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_3D_EFFECTS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a273d7684614ee495426b436317a30fa0ce2d59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333311"
---
# <a name="ksnodetype3deffects"></a>KSNODETYPE\_3D\_効果


## <span id="ddk_ksnodetype_3d_effects_ks"></span><span id="DDK_KSNODETYPE_3D_EFFECTS_KS"></span>


KSNODETYPE\_3D\_効果ノードは、基になるデバイスに固有 3D HAL (ハードウェアの高速化レイヤー) の 3D 効果のプロセッサを表します、 **IDirectSound3DBuffer**と**IDirectSound3DListener** Api (Microsoft Windows SDK のドキュメントで説明)。 3D のノードが 1 つまたは 2 つのいずれかのチャネルの 1 つの入力ストリームと 1 つの出力をストリーム*n*チャネル。 出力ストリームの 3D サウンド フィールド内で個々 のチャネルの入力ストリームを配置します。

通常、3 D のノードに入力ストリームには、1 つのチャネルが含まれています。 DirectSound 8.0 以降では、mono PCM バッファーのみを 3D 効果を作成できます。 以前のバージョン、DirectSound が、mono とステレオの両方の入力ストリームと 3D のノードをサポートし、ドライバーは古いバージョンのアプリケーションとの互換性を確保するために両方をサポートする必要があります。

KSNODETYPE\_3D\_効果ノードは、次の省略可能なプロパティを使用して、DirectSound スピーカー構成の制御に使用されます。

[**KSPROPERTY\_オーディオ\_チャネル\_構成**](ksproperty-audio-channel-config.md)

[**KSPROPERTY\_AUDIO\_STEREO\_SPEAKER\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)

詳細については、次を参照してください。 [DirectSound スピーカー構成設定](https://msdn.microsoft.com/library/windows/hardware/ff536332)します。

さらに、DirectSound いる必要があります、KSNODETYPE\_3D\_効果ノードは、次の 3 D リスナーと 3D バッファー プロパティをサポートします。

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_ALL**](ksproperty-directsound3dbuffer-all.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_位置**](ksproperty-directsound3dbuffer-position.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_ベロシティ**](ksproperty-directsound3dbuffer-velocity.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES**](ksproperty-directsound3dbuffer-coneangles.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEORIENTATION**](ksproperty-directsound3dbuffer-coneorientation.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME**](ksproperty-directsound3dbuffer-coneoutsidevolume.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE**](ksproperty-directsound3dbuffer-mindistance.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MAXDISTANCE**](ksproperty-directsound3dbuffer-maxdistance.md)

[**KSPROPERTY\_DIRECTSOUND3DBUFFER\_MODE**](ksproperty-directsound3dbuffer-mode.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ALL**](ksproperty-directsound3dlistener-all.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_位置**](ksproperty-directsound3dlistener-position.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ベロシティ**](ksproperty-directsound3dlistener-velocity.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_向き**](ksproperty-directsound3dlistener-orientation.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR**](ksproperty-directsound3dlistener-rollofffactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_意味**](ksproperty-directsound3dlistener-dopplerfactor.md)

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_バッチ**](ksproperty-directsound3dlistener-batch.md)

KSNODETYPE\_3D\_効果ノードがヘッド相対転送関数 (HRTF) を実装、その場合、次の省略可能なプロパティをサポートすること。

[**KSPROPERTY\_HRTF3D\_フィルター\_形式**](ksproperty-hrtf3d-filter-format.md)

[**KSPROPERTY\_HRTF3D\_初期化**](ksproperty-hrtf3d-initialize.md)

[**KSPROPERTY\_HRTF3D\_PARAMS**](ksproperty-hrtf3d-params.md)

KSNODETYPE\_3D\_効果ノードは、両耳間時間の遅延 (ITD) アルゴリズムを実装できますが、この場合は、次の省略可能なプロパティをサポートする必要があります。

[**KSPROPERTY\_ITD3D\_PARAMS**](ksproperty-itd3d-params.md)

 

 





