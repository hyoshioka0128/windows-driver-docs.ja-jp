---
title: パレット化テクスチャ
description: パレット化テクスチャ
ms.assetid: eac46256-db08-4a9b-aaaf-2bc8a9f30e98
keywords:
- テクスチャ管理 WDK Direct3D でパレット化されたテクスチャ
- パレット化されたテクスチャ WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 654754328601f3a8e0f8ec05299dab4d2330cd00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377361"
---
# <a name="paletted-textures"></a>パレット化テクスチャ


## <span id="ddk_paletted_textures_gg"></span><span id="DDK_PALETTED_TEXTURES_GG"></span>


Direct3D は、テクスチャで使用するパレットを使用できます。 パレットは、その他のオブジェクトの DirectDrawSurface することと同様、テクスチャに接続できます。 パレット化されたテクスチャをサポートするために、ドライバーが、D3DDP2OP に応答する必要があります\_SETPALETTE と D3DDP2OP\_UPDATEPALETTE 操作のコードの実装で[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb). これらの操作コードが続いて[ **D3DHAL\_DP2SETPALETTE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setpalette)と[ **D3DHAL\_DP2UPDATEPALETTE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2updatepalette)構造、それぞれに、コマンドのストリームにします。 D3DDP2OP\_SETPALETTE パレット ハンドルとサーフェスのハンドルの間のアソシエーションを作成する (既にによって作成された[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex))。 その後、D3DDP2OP\_UPDATEPALETTE は、このテクスチャのパレット エントリの値の設定を複数回送信することができます。

 

 





