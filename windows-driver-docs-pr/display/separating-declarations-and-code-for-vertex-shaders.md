---
title: 頂点シェーダーの宣言とコードの分離
description: 頂点シェーダーの宣言とコードの分離
ms.assetid: 6da26a8f-553b-4995-9dda-66a7fd6d478b
keywords:
- 頂点シェーダーの宣言 WDK DirectX 9.0、宣言とコードの分離
- シェーダー宣言 WDK DirectX 9.0、宣言とコードの分離
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf7270efd6804e3b21476e13ac6429d90fc29ea3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829505"
---
# <a name="separating-declarations-and-code-for-vertex-shaders"></a>頂点シェーダーの宣言とコードの分離


## <span id="ddk_separating_declarations_and_code_for_vertex_shaders_gg"></span><span id="DDK_SEPARATING_DECLARATIONS_AND_CODE_FOR_VERTEX_SHADERS_GG"></span>


DirectX 9.0 では、頂点シェーダーが作成されるときに、頂点シェーダーの宣言とコードが結合されなくなりました。 頂点シェーダーをサポートするデバイスの DirectX 9.0 バージョンドライバーは、宣言およびコードオブジェクトの個別の作成と管理を処理する必要があります。 ただし、この DirectX 9.0 ドライバーは、宣言とコードの両方を組み合わせた頂点シェーダーオブジェクトを引き続き管理できなければなりません。これは、DirectX 8.0 ランタイムがこのような頂点シェーダーオブジェクトの作成を要求する場合があるためです。 詳細については、「[頂点シェーダー](vertex-shaders.md)」を参照してください。

DirectX 9.0 ランタイムは、個別のハンドルプールから宣言とコードオブジェクトの両方にハンドルを割り当てます。 DirectX 9.0 ドライバーは、これらのハンドルを別々の配列に格納する必要があります。 Directx 8.0 の頂点シェーダーハンドル空間と同様に、DirectX 9.0 では、頂点シェーダー宣言のハンドル空間が、フレキシブル頂点形式 (FVF) コードによって共有されます。 ハンドルのビットゼロを設定すると、頂点シェーダーの宣言が示されます。それ以外の場合は、FVF コードを指定します。 詳細については、リファレンスラスタライザー (「参照」*のサンプルコード*) を参照してください。

DirectX 9.0 ドライバーは、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数で D3DDP2OP\_CREATEVERTEXSHADERDECL operation コードを処理するときに、頂点シェーダー宣言を受け取ります。 [**D3DHAL\_DP2CREATEVERTEXSHADERDECL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2createvertexshaderdecl)構造体と、シェーダー宣言を構成する頂点要素を定義する D3DVERTEXELEMENT9 構造体の配列は、[コマンドストリーム](command-stream.md)の操作コードに従います。 シェーダー宣言の頂点要素を処理するために DirectX 9.0 ドライバーが実装されている場合は、頂点データのすべての使用可能な使用をサポートする必要があります。 つまり、これらの型の複数の意味 (使用状況インデックス値) と共に、すべての D3DDECLUSAGE 型をサポートする必要があります。 D3DVERTEXELEMENT9 と D3DDECLUSAGE の詳細については、最新の DirectX SDK のドキュメントを参照してください。

DirectX 9.0 ドライバーは、D3DDP2OP\_CREATEVERTEXSHADERFUNC 操作コードを処理するときに、頂点シェーダーコードを受け取ります。 [**D3DHAL\_DP2CREATEVERTEXSHADERFUNC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2createvertexshaderfunc)構造体と頂点シェーダーコードは、コマンドストリームの操作コードに従います。 個々のシェーダーコードの形式と各シェーダーコードを構成するトークンの詳細については、「 [Direct3D ドライバーのシェーダーコード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

DirectX 9.0 ドライバーは、D3DDP2OP\_SETVERTEXSHADERDECL および D3DDP2OP\_SETVERTEXSHADERFUNC 操作コードを処理して、頂点シェーダーアセンブラーで特定の頂点シェーダー宣言とコードを最新のものにします。 ドライバーは、D3DDP2OP\_DELETEVERTEXSHADERDECL および D3DDP2OP\_DELETEVERTEXSHADERFUNC 操作コードを処理して、これらの頂点シェーダーの宣言とコードを頂点シェーダーアセンブラーから削除します。 これらの各操作コードについて、コマンドストリームの[**D3DHAL\_DP2VERTEXSHADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2vertexshader)構造体は次のようになります。 この構造体には、設定または削除する宣言またはコードへのハンドルを識別するメンバーが1つだけ含まれています。

 

 





