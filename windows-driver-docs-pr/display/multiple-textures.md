---
title: 複数のテクスチャ
description: 複数のテクスチャ
ms.assetid: 3c7b4ac7-eabc-442d-aede-a65ee3b6e20c
keywords:
- テクスチャ管理 WDK Direct3D、複数のテクスチャ
- 複数のテクスチャ WDK Direct3D
- 複数のテクスチャの複数のテクスチャ WDK Direct3D、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0db9f880772611ed4572d1d9e0ca9cbefcb6f650
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345582"
---
# <a name="multiple-textures"></a>複数のテクスチャ


## <span id="ddk_multiple_textures_gg"></span><span id="DDK_MULTIPLE_TEXTURES_GG"></span>


Direct3D のドライバーでは、テクスチャ ステージ状態の種類は、DirectX SDK のドキュメントで説明されている、D3DTEXTURESTAGESTATETYPE のテクスチャ ステージの状態を使用して複数のテクスチャの同時使用をサポートできます。 この型を定義し、独立したテクスチャ座標のデータのセットを指定する頂点の拡張機能と組み合わせて、テクスチャのすべてのプロパティを使用します。

Direct3D のドライバーの複数のテクスチャのサポートを追加する場合は、テクスチャのブレンドと実装を実装する正しい機能ビット (Cap) を設定する必要があります[ **D3dValidateTextureStageState**](https://msdn.microsoft.com/library/windows/hardware/ff549064)します。

DirectX 6.0 およびそれ以降のバージョンに準拠するには、ドライバーは、デバイスが反復処理するのみとで定義されている座標の数を使用できる場合でも、最大 8 つのテクスチャ座標セットを正しく解析するために必要、 **dwFVFCaps**のメンバー、[ **D3DHAL\_D3DEXTENDEDCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff544753)構造体。 ドライバーが使用 D3DTSS\_TEXCOORDINDEX テクスチャ リングに使用する適切な座標を取得します。

柔軟な頂点の形式 ([FVF](fvf--flexible-vertex-format-.md)) ができることに、頂点構造体では、複数のテクスチャ座標を渡すために複数のテクスチャを許可します。 複数のテクスチャをブレンド繰り返し行う一連のプロセスとジオメトリの一部に適用します。

テクスチャのハンドルは Direct3D ドライバーによって生成されません。 代わりに、テクスチャのハンドルは、Direct3D ランタイムによって生成されます。 テクスチャのキャッシュ管理は、ドライバーのテクスチャ常に表示されるように、アプリケーション自体に由来する、Direct3D ランタイムによって完全に行われます。 すべてのテクスチャの状態がドライバーに送信される、 [ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)コマンド ストリーム。

複数のテクスチャの追加により、ブレンドして、テクスチャ フィルタ リングする方法も改良されてきたブレンドをわかりやすくより明確に定義されたメカニズムを提供します。 これらのブレンドとテクスチャのメカニズムをフィルタ リングする方法の詳細については、Microsoft DirectX SDK ドキュメントを参照してください。

ドライバーの設定、D3DDEVCAPS 場合\_SEPARATETEXTUREMEMORIES フラグ、 **DevCaps**に DirectX 8.0、およびそれ以降のバージョンのアプリケーションから無効になっていることを示します D3DCAPS8 構造体のメンバーは、同時に複数のテクスチャを使用します。 ドライバーがへの応答で D3DCAPS8 構造体を返します、 **GetDriverInfo2** 」の説明に従ってクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

 

 





