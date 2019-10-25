---
title: ボリューム テクスチャに対するサポートのレポート
description: ボリューム テクスチャに対するサポートのレポート
ms.assetid: da0c1c88-504e-4293-96ca-65cac2e0fe97
keywords:
- テクスチャ WDK DirectX 8.0
- DirectX 8.0 リリースノート WDK Windows 2000 display、volume テクスチャ
- ボリュームテクスチャ WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 941c0f411d56f1159a682bc6c3478ac3d704d41b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829578"
---
# <a name="reporting-support-for-volume-textures"></a>ボリューム テクスチャに対するサポートのレポート


## <span id="ddk_reporting_support_for_volume_textures_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_VOLUME_TEXTURES_GG"></span>


DirectX 8.0 では、ドライバーがボリュームテクスチャのサポートを示すために設定する2つの新しいプリミティブテクスチャ機能フラグが導入されています。 これらのフラグは、D3DPTEXTURECAPS\_VOLUMEMAP と D3DPTEXTURECAPS\_MIPVOLUMEMAP になります。 ハードウェアがボリュームテクスチャをサポートしている場合は、D3DPRIMCAPS8 構造体 (D3DCAPS8 の一部) の**Dwtexturecaps**フィールドに D3DPTEXTURECAPS\_volumemap を設定する必要があります。 D3DPTEXTURECAPS\_MIPVOLUMEMAP は、ドライバーが MIP マップボリュームテクスチャをサポートしていることを示します。

ボリュームテクスチャをサポートするハードウェアでは、マルチテクスチャのシナリオでのボリュームテクスチャの使用もサポートする必要があります (他のボリュームテクスチャや2D テクスチャと組み合わせて)。 このシナリオがハードウェアでサポートされていない場合、ドライバーは D3DPTEXTURECAPS\_VOLUMEMAP を設定できません。

ドライバーは、プリミティブテクスチャ機能 D3DPTEXTURECAPS\_VOLUMEMAP\_POW2 に設定することによって、ボリュームテクスチャの大きさを2の累乗にする必要があることを示している可能性があります。

ボリュームテクスチャをサポートするドライバーは、サポートされる最小および最大のボリュームテクスチャの寸法を指定するためにも必要です。 **Maxvolumeextent**フィールドは、ボリュームテクスチャのサポートされている最大サイズに設定する必要があります。 同じ制約は、ボリュームテクスチャの3次元すべて (幅、高さ、および深度) に適用する必要があります。

ドライバーは、ボリュームテクスチャのフィルター処理と、ハードウェアでサポートされているテクスチャのアドレス指定モードをランタイムに通知します。これを行うには、 **volumetexを**適切なフラグの**組み合わせに設定**します。

最後に、ドライバーは、surface 形式の[**Ddのピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)の**dwoperations**フィールドで D3DFORMAT\_OP\_volumetexture を設定することによって、ボリュームテクスチャで使用できるサーフェイス形式をランタイムに通知します。

 

 





