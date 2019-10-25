---
title: テクスチャリング要件
description: テクスチャリング要件
ms.assetid: 5fb64c9e-1c6d-4a8a-9a8f-7d4ed6d5c301
keywords:
- テクスチャサイズ WDK Direct3D
- テクスチャフィルター WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40ee891258aa4e53b15cedee0fb334abc09fa18f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829330"
---
# <a name="texturing-requirements"></a>テクスチャリング要件


## <span id="ddk_texturing_requirements_gg"></span><span id="DDK_TEXTURING_REQUIREMENTS_GG"></span>


このセクションでは、テクスチャのサイズとテクスチャのフィルター処理に関する要件を示します。 **IDirect3DDevice7:: ValidateDevice**メソッドには、テクスチャ関連の要件もあります。

### <a name="span-idtexture_sizesspanspan-idtexture_sizesspantexture-sizes"></a><span id="texture_sizes"></span><span id="TEXTURE_SIZES"></span>テクスチャのサイズ

テクスチャサイズの要件を次に示します。

1.  ドライバーは、D3DDEVICEDESC7 構造体の**dwMinTextureWidth**、 **dwMinTextureHeight**、 **dwMaxTextureWidth**、 **dwMaxTextureHeight**の各メンバーを介して、最小テクスチャおよび最大テクスチャの寸法を公開する必要があります。 この構造体は、Direct3D SDK ドキュメントで定義されています。

2.  ハードウェアのテクスチャに縦横比の制限がある場合、その比率は D3DDEVICEDESC7 構造体の**dwMaxTextureAspectRatio**メンバーに存在する必要があります。

3.  デバイスが2の累乗であるテクスチャ寸法のみをサポートしている場合は、 [**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**Dwtexturecaps**メンバー\_を設定して、適切なプリミティブ型 (行または三角形)。

4.  テクスチャステージのテクスチャアドレッシングモードが D3DTADDRESS\_クランプに設定されている場合、デバイスが任意のサイズの2次元 (2D) テクスチャをサポートできる場合は、テクスチャステージのテクスチャの折り返しが無効になります (D3DRENDERSTATE\_WRAP*n*を0に設定)、MIP マッピングが使用されていない場合は、D3DPTEXTURECAPS\_NONPOW2CONDITIONAL フラグを設定する必要があります。

5.  デバイスが、次元が等しいテクスチャのみをサポートしている場合は、 [**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造\_体の**Dwtexturecaps**メンバーを設定して、適切なプリミティブ型 (行または三角形)。

1番目と2番目の要件に記載されているもの以外の制限なく、任意のサイズのテクスチャがサポートされる場合は、3番目、4番目、および5番目の要件で説明されているフラグを設定しないようにする必要があります。

### <a name="span-idtexture_filteringspanspan-idtexture_filteringspantexture-filtering"></a><span id="texture_filtering"></span><span id="TEXTURE_FILTERING"></span>テクスチャのフィルター処理

テクスチャを拡大および縮小するフィルターは、D3DTSS\_MAGFILTER と D3DTSS\_MINFILTER テクスチャステージの状態によって有効または無効にする必要があります。 これらの状態が無効になっている場合は、このフィルター処理を自動的に実行しないでください。 D3DTSS\_*Xxx*のテクスチャステージの状態の詳細については、Direct3D SDK ドキュメントの「D3DTEXTURESTAGESTATETYPE 列挙型」を参照してください。

テクスチャ MIP マッピングは、D3DTSS\_MIPFILTER テクスチャステージの状態で有効にし、無効にする必要があります。 この状態が無効になっていても、テクスチャが MIP マップとして作成された場合、デバイスは MIP マップの最上位レベルのみを使用する必要があります。 この状態が無効になっている場合は、MIP マップフィルターを実行しないでください。

デバイスで異方性フィルターがサポートされている場合は、異方性の最大レベルを、D3DDEVICEDESC7 構造体の**dwMaxAnisotropy**メンバー (Direct3D SDK ドキュメントで定義) の値を使用してエクスポートする必要があります。 さらに、デバイスは、D3DTSS\_MAXANISOTROPY テクスチャステージの状態で、1 ~ **dwMaxAnisotropy**の設定を受け入れる必要があります。

デバイスは、サポートされているすべてのフィルターモードを、サポートされている任意の形式のテクスチャに適用できる必要があります。 たとえば、MIP マッピングが他のテクスチャ形式でサポートされている場合、YUV テクスチャの MIP マップフィルター処理を実行できる必要があります。

**   DirectX** 9.0 以降のアプリケーションでは、D3DSAMPLERSTATETYPE 列挙体の値を使用して、サンプラーテクスチャ関連のレンダリング状態の特性を制御できます。 DirectX 8.0 以前では、これらのサンプラーの状態は D3DTEXTURESTAGESTATETYPE 列挙体に含まれていました。 ランタイムは、ユーザーモードサンプラーの状態 (D3DSAMP\_*Xxx*) をカーネルモードの D3DTSS\_*xxx*値にマップして、ドライバーがユーザーモードのサンプラー状態を処理する必要がないようにします。 D3DSAMPLERSTATETYPE の詳細については、最新の DirectX SDK のドキュメントを参照してください。

 

### <a name="span-ididirect3ddevice7_validatedevicespanspan-ididirect3ddevice7_validatedevicespanidirect3ddevice7validatedevice"></a><span id="idirect3ddevice7_validatedevice"></span><span id="IDIRECT3DDEVICE7_VALIDATEDEVICE"></span>IDirect3DDevice7:: ValidateDevice

デバイスが1回のパスでのテクスチャステージ状態のブレンド操作とオペランドの特定の組み合わせをサポートしている場合、デバイスは**IDirect3DDevice7:: ValidateDevice**メソッドの呼び出しから DD\_OK を返す必要があります (「Direct3D SDK」で説明しています)。ドキュメント) を参照してください。

1つのパスでのテクスチャステージ状態のブレンド操作の特定の組み合わせがデバイスでサポートされていない場合、または1つ以上のブレンド操作またはオペランドがサポートされていない場合は、IDirect3DDevice7 で使用できるエラーコードの1つを返す必要があり**ます。: ValidateDevice**メソッド。 無効なブレンド操作では、 **IDirect3DDevice7:: ValidateDevice**メソッドをサイレントに失敗させることはできません。

 

 





