---
title: ボリューム テクスチャに対するサポートのレポート
description: ボリューム テクスチャに対するサポートのレポート
ms.assetid: da0c1c88-504e-4293-96ca-65cac2e0fe97
keywords:
- WDK DirectX 8.0 のテクスチャ
- Windows 2000 の WDK の表示、ボリュームのテクスチャの DirectX 8.0 リリース ノートします。
- ボリューム テクスチャ WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2c68658eb0e80da5da356bf2c073642a1f275ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571633"
---
# <a name="reporting-support-for-volume-textures"></a>ボリューム テクスチャに対するサポートのレポート


## <span id="ddk_reporting_support_for_volume_textures_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_VOLUME_TEXTURES_GG"></span>


DirectX 8.0 ではボリューム テクスチャのサポートを示すため、ドライバーを設定する 2 つの新しいプリミティブ テクスチャ機能フラグが導入されています。 これらのフラグは D3DPTEXTURECAPS\_VOLUMEMAP と D3DPTEXTURECAPS\_MIPVOLUMEMAP します。 D3DPTEXTURECAPS\_VOLUMEMAP 設定する必要があります、 **dwTextureCaps** D3DPRIMCAPS8 構造 (D3DCAPS8 の一部) の場合、ハードウェアはボリューム テクスチャのサポート フィールド。 D3DPTEXTURECAPS\_MIPVOLUMEMAP はボリューム テクスチャが MIP ドライバーのサポートにマップされていることを示します。

ボリューム テクスチャをサポートするハードウェアでは、(他のボリューム テクスチャまたはテクスチャ 2D と組み合わせて) マルチ テクスチャ リングのシナリオでもボリューム テクスチャの使用をサポートする必要があります。 このシナリオは、ハードウェアでサポートされていない、ドライバーは D3DPTEXTURECAPS を設定できません\_VOLUMEMAP します。

D3DPTEXTURECAPS プリミティブ テクスチャ機能を設定して 2 の累乗であることをボリューム テクスチャの大きさが必要である、ドライバーが分かります\_VOLUMEMAP\_POW2 します。

ボリューム テクスチャをサポートしているドライバーがサポートされる最小値と最大ボリューム テクスチャの大きさを指定するも必要です。 フィールド**MaxVolumeExtent**ボリューム テクスチャのサポートされている最大サイズに設定する必要があります。 ボリュームのテクスチャ (幅、高さ、深度) の 3 つすべてのディメンションに同じ制約を適用する必要があります。

ドライバーはボリューム テクスチャ フィルタ リングとテクスチャを設定して、ハードウェアでサポートされるモードをアドレス指定のランタイムを通知、 **VolumeTextureFilterCaps**と**VolumeTextureAddressCaps**に、フラグの適切な組み合わせです。

最後に、ドライバーに通知についてどのような画面が書式設定、ランタイムは、設定、D3DFORMAT ボリューム テクスチャで使用できる\_OP\_で VOLUMETEXTURE、 **dwOperations**サーフェイス形式ののフィールド[**DDPIXELFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff550274)します。

 

 





