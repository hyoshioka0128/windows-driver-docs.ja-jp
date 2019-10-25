---
title: パレット化テクスチャ
description: パレット化テクスチャ
ms.assetid: eac46256-db08-4a9b-aaaf-2bc8a9f30e98
keywords:
- テクスチャ管理 WDK Direct3D、パレット化テクスチャ
- パレット化テクスチャ WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b26f160f67ab5f59aa1e31eb9cece0afa7454638
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826060"
---
# <a name="paletted-textures"></a>パレット化テクスチャ


## <span id="ddk_paletted_textures_gg"></span><span id="DDK_PALETTED_TEXTURES_GG"></span>


Direct3D では、パレットをテクスチャと共に使用できます。 パレットは、他の DirectDrawSurface オブジェクトと同じように、テクスチャに関連付けることができます。 パレット化されたテクスチャをサポートするには、ドライバーが[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)の実装の D3DDP2OP\_setpalette および D3DDP2OP\_updatepalette 操作コードに応答する必要があります。 これらの操作コードの後には、コマンドストリームで[**D3DHAL\_DP2SETPALETTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setpalette)と[**D3DHAL\_DP2UPDATEPALETTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2updatepalette)構造体がそれぞれ続きます。 D3DDP2OP\_SETPALETTE は、パレットハンドルと surface ハンドル ( [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)によって作成済み) の間の関連付けを作成します。 後で、D3DDP2OP\_UPDATEPALETTE を複数回送信して、このテクスチャのパレットエントリの値を設定できます。

 

 





