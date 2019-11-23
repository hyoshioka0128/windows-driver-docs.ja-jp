---
title: FVF (柔軟な頂点形式)
description: FVF (柔軟な頂点形式)
ms.assetid: 206f4275-bcb8-4e8e-9c11-c6fb5d9c561d
keywords:
- 頂点形式 WDK Direct3D
- 柔軟な頂点形式 WDK Direct3D
- FVF WDK Direct3D
- Direct3D WDK Windows 2000 display、フレキシブル頂点形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b4177393c592b878f622f9bc57415e3d93b34a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838937"
---
# <a name="fvf-flexible-vertex-format"></a>FVF (柔軟な頂点形式)


## <span id="ddk_fvf_gg"></span><span id="DDK_FVF_GG"></span>


ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コールバックは、頂点データを柔軟な頂点形式 (FVF) で受信します。 頂点の形式は柔軟なので、このデータに対しては包括的なデータ構造が定義されていません。 ドライバーは、完全な FVF 機能を実装する必要があります。

通常の2D テクスチャに加えて、1D、3D、4D の各テクスチャを含む、Microsoft DirectX 7.0 用の FVF 更新プログラムがあります。 この更新プログラムの詳細については、「 [FVF update](fvf-update.md)」を参照してください。 これらのトピックの詳細については、 *Perm3*サンプルドライバーおよび DirectX SDK のドキュメントを参照してください。

Microsoft Windows Driver Kit (WDK) には、3Dlabs Permedia3 sample display Driver (*Perm3*) が含まれていない  **ことに注意**してください。 このサンプルドライバーは、Windows Server 2003 SP1 Driver Development Kit (DDK) から入手できます。このドライバーは、WDHC web サイトの DDK-Windows Driver Development Kit ページからダウンロードできます。

 

 

 





