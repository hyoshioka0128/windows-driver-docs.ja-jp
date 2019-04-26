---
title: パレット化テクスチャ
description: パレット化テクスチャ
ms.assetid: eac46256-db08-4a9b-aaaf-2bc8a9f30e98
keywords:
- テクスチャ管理 WDK Direct3D でパレット化されたテクスチャ
- パレット化されたテクスチャ WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087b804e25d8336a01ea9a14558fa457d9fe548e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352392"
---
# <a name="paletted-textures"></a>パレット化テクスチャ


## <span id="ddk_paletted_textures_gg"></span><span id="DDK_PALETTED_TEXTURES_GG"></span>


Direct3D は、テクスチャで使用するパレットを使用できます。 パレットは、その他のオブジェクトの DirectDrawSurface することと同様、テクスチャに接続できます。 パレット化されたテクスチャをサポートするために、ドライバーが、D3DDP2OP に応答する必要があります\_SETPALETTE と D3DDP2OP\_UPDATEPALETTE 操作のコードの実装で[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704). これらの操作コードが続いて[ **D3DHAL\_DP2SETPALETTE** ](https://msdn.microsoft.com/library/windows/hardware/ff545744)と[ **D3DHAL\_DP2UPDATEPALETTE** ](https://msdn.microsoft.com/library/windows/hardware/ff545923)構造、それぞれに、コマンドのストリームにします。 D3DDP2OP\_SETPALETTE パレット ハンドルとサーフェスのハンドルの間のアソシエーションを作成する (既にによって作成された[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840))。 その後、D3DDP2OP\_UPDATEPALETTE は、このテクスチャのパレット エントリの値の設定を複数回送信することができます。

 

 





