---
title: 複数のテクスチャ
description: 複数のテクスチャ
ms.assetid: 3c7b4ac7-eabc-442d-aede-a65ee3b6e20c
keywords:
- テクスチャ管理 WDK Direct3D、複数のテクスチャ
- 複数のテクスチャ WDK Direct3D
- 複数のテクスチャ WDK Direct3D、複数のテクスチャについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7637f2d3a759c68341f491dcd8b6f69d681ee57
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840534"
---
# <a name="multiple-textures"></a>複数のテクスチャ


## <span id="ddk_multiple_textures_gg"></span><span id="DDK_MULTIPLE_TEXTURES_GG"></span>


Direct3D ドライバーは、DirectX SDK のドキュメントで説明されているテクスチャステージ状態の種類 D3DTEXTURESTAGESTATETYPE のテクスチャステージの状態を使用して、複数のテクスチャを同時に使用することをサポートできます。 この型を使用すると、テクスチャのすべてのプロパティを定義し、テクスチャ座標データの独立したセットを指定する頂点拡張機能と組み合わせることができます。

Direct3D ドライバーの複数のテクスチャサポートを追加するには、正しい機能ビット (Caps) を設定し、テクスチャブレンドを実装し、 [**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)を実装する必要があります。

DirectX 6.0 以降のバージョンに準拠するためには、デバイスが D3DHAL の**dwFVFCaps**メンバーで定義されている座標の数のみを反復して使用できる場合でも、ドライバーは最大8個のテクスチャ座標セットを適切に解析する必要があり[ **\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)構造体。 ドライバーは、D3DTSS\_TEXCOORDINDEX を使用して、テクスチャに使用する正しい座標を取得します。

フレキシブル頂点形式 ([FVF](fvf--flexible-vertex-format-.md)) を使用すると、複数のテクスチャ座標を頂点構造に渡すことができるため、複数のテクスチャ処理が可能になります。 その後、複数のテクスチャを反復処理でブレンドし、ジオメトリに適用することができます。

テクスチャハンドルは、Direct3D ドライバーでは生成されなくなりました。 代わりに、テクスチャハンドルは Direct3D ランタイムによって生成されます。 テクスチャキャッシュ管理は、Direct3D ランタイムによって完全に実行されるため、ドライバーに対しては、テクスチャは常にアプリケーション自体から取得されるように見えます。 すべてのテクスチャの状態は、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コマンドストリームのドライバーに送信されます。

複数のテクスチャを追加することで、ブレンドとテクスチャフィルター処理のためのメソッドも改良され、より明確で明確に定義されたブレンドメカニズムが提供されます。 これらのブレンドとテクスチャのフィルター処理メカニズムの詳細については、Microsoft DirectX SDK のドキュメントを参照してください。

ドライバーが D3DCAPS8 構造体の**Devcaps**メンバーで D3DDEVCAPS\_SEPARATETEXTUREMEMORIES フラグを設定した場合は、DirectX 8.0 以降のバージョンのアプリケーションに対して、複数のテクスチャを使用して同時に無効にすることを示します。 このドライバーは、「 [DirectX 8.0 スタイルの Direct3D 機能の報告](reporting-directx-8-0-style-direct3d-capabilities.md)」で説明されているように、 **GetDriverInfo2**クエリに応答して D3DCAPS8 構造体を返します。 このクエリのサポートについては、「 [GetDriverInfo2](supporting-getdriverinfo2.md)のサポート」を参照してください。

 

 





