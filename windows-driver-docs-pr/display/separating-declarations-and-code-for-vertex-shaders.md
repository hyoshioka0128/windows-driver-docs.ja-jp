---
title: 頂点シェーダーの宣言とコードの分離
description: 頂点シェーダーの宣言とコードの分離
ms.assetid: 6da26a8f-553b-4995-9dda-66a7fd6d478b
keywords:
- 頂点シェーダー宣言 WDK DirectX 9.0、宣言とコードの分離
- シェーダー宣言 WDK DirectX 9.0、宣言とコードの分離
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a238a2c879394305c813f3b9ecb89084446559b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390485"
---
# <a name="separating-declarations-and-code-for-vertex-shaders"></a>頂点シェーダーの宣言とコードの分離


## <span id="ddk_separating_declarations_and_code_for_vertex_shaders_gg"></span><span id="DDK_SEPARATING_DECLARATIONS_AND_CODE_FOR_VERTEX_SHADERS_GG"></span>


DirectX 9.0、宣言と頂点シェーダーのコード不要になった結合頂点シェーダーの作成時にされます。 頂点シェーダーをサポートするデバイスの DirectX 9.0 バージョンのドライバーには、個別の作成とオブジェクトの宣言とコードの管理を処理する必要があります。 ただし、この DirectX 9.0 ドライバーを 8.0 の DirectX のランタイムを頂点シェーダー オブジェクトを作成する要求がありますので、宣言と、コードの両方を組み合わせて、頂点シェーダー オブジェクトを管理できるようにする必要があります。 詳細については、次を参照してください。[頂点シェーダー](vertex-shaders.md)します。

DirectX 9.0 ランタイムは、宣言とコード オブジェクトの両方に、別のハンドルのプールからハンドルを割り当てます。 DirectX 9.0 ドライバーは、個別の配列でこれらのハンドルを格納する必要があります。 頂点シェーダーは、DirectX 8.0 で領域を処理するように、DirectX 9.0 は柔軟な頂点の書式 (FVF) コードと頂点シェーダーの宣言のハンドルの領域を共有します。 ハンドルのビットが 0 を設定するコードを示します頂点シェーダー宣言では、それ以外の場合、FVF。 詳細については、リファレンス ラスタライザーを参照してください (*refrast.cpp*サンプル コード)。

DirectX 9.0 ドライバーが、D3DDP2OP を処理するときに、頂点シェーダーの宣言を受け取る\_CREATEVERTEXSHADERDECL 操作のコードでその[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)関数。 A [ **D3DHAL\_DP2CREATEVERTEXSHADERDECL** ](https://msdn.microsoft.com/library/windows/hardware/ff545480)構造とシェーダーの宣言を構成する頂点の要素を定義する D3DVERTEXELEMENT9 構造体の配列の次の操作コードで、[コマンド ストリーム](command-stream.md)します。 シェーダーの宣言の頂点の要素を処理する DirectX 9.0 ドライバーが実装されている場合は、頂点データのすべての可能な使用をサポートしてする必要があります。 これらの種類と共に複数の意味があります (使用状況インデックス値) のすべての D3DDECLUSAGE 型をサポートしてする必要があります。 D3DVERTEXELEMENT9 と D3DDECLUSAGE する方法の詳細については、DirectX SDK の最新のドキュメントを参照してください。

DirectX 9.0 ドライバーが、D3DDP2OP を処理するときに、頂点シェーダー コードを受け取る\_CREATEVERTEXSHADERFUNC 操作コード。 A [ **D3DHAL\_DP2CREATEVERTEXSHADERFUNC** ](https://msdn.microsoft.com/library/windows/hardware/ff545490)構造と頂点シェーダーのコードがコマンド ストリーム内で操作コードに従ってください。 個々 のシェーダー コードの各シェーダー コードを構成するトークン形式の詳細については、次を参照してください。 [Direct3D ドライバーのシェーダー コード](https://msdn.microsoft.com/library/windows/hardware/ff552855)します。

DirectX 9.0 ドライバーの処理、D3DDP2OP\_SETVERTEXSHADERDECL と D3DDP2OP\_させる特定の頂点シェーダーの宣言とコードの現在の頂点シェーダー アセンブラー SETVERTEXSHADERFUNC オペレーション コード。 ドライバーの処理、D3DDP2OP\_DELETEVERTEXSHADERDECL と D3DDP2OP\_頂点シェーダー アセンブラーからこれらの頂点シェーダーの宣言とコードを削除する DELETEVERTEXSHADERFUNC オペレーション コード。 これらの操作コードの各、 [ **D3DHAL\_DP2VERTEXSHADER** ](https://msdn.microsoft.com/library/windows/hardware/ff545925)コマンド ストリームの構造に依存します。 この構造体には、宣言または設定または削除するコードを識別するハンドルを識別する 1 つのメンバーが含まれています。

 

 





