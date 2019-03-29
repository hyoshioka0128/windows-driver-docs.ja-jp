---
title: テクスチャリング要件
description: テクスチャリング要件
ms.assetid: 5fb64c9e-1c6d-4a8a-9a8f-7d4ed6d5c301
keywords:
- WDK Direct3D テクスチャのサイズ
- テクスチャの WDK Direct3D をフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b34531b6cda8db7e19d9b0c9175e391c360237d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572409"
---
# <a name="texturing-requirements"></a>テクスチャリング要件


## <span id="ddk_texturing_requirements_gg"></span><span id="DDK_TEXTURING_REQUIREMENTS_GG"></span>


このセクションでは、テクスチャのサイズとテクスチャ フィルタ リングするための要件を示します。 テクスチャに関連する要件がある、 **IDirect3DDevice7::ValidateDevice**メソッド。

### <a name="span-idtexturesizesspanspan-idtexturesizesspantexture-sizes"></a><span id="texture_sizes"></span><span id="TEXTURE_SIZES"></span>テクスチャのサイズ

以下は、テクスチャのサイズの要件です。

1.  ドライバーを通じてその最小値と最大のテクスチャのディメンションを公開する必要があります、 **dwMinTextureWidth**、 **dwMinTextureHeight**、 **dwMaxTextureWidth**、および**dwMaxTextureHeight** D3DDEVICEDESC7 構造体のメンバー。 この構造体は、Direct3D SDK のドキュメントで定義されます。

2.  そのテクスチャでのハードウェアに縦横比 に制限した場合、その比率が必要である、 **dwMaxTextureAspectRatio** D3DDEVICEDESC7 構造体のメンバー。

3.  デバイス 2 の累乗であるだけのテクスチャのディメンションをサポートするかどうかは、設定する必要がありますが、 **dwTextureCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)格納する構造体、D3DPTEXTURECAPS\_POW2 フラグの適切なプリミティブ型 (線または三角形)。

4.  D3DTADDRESS にテクスチャ ステージのテクスチャのアドレッシング モードが設定されている場合、デバイスが任意のサイズの 2 次元 (2 D) テクスチャ (つまり、ボリュームではなくまたはキューブのテクスチャ) をサポートできる場合\_クランプ、テクスチャのステージのテクスチャのラッピングが無効になっています (D3DRENDERSTATE\_ラップ*n*を 0 に設定)、MIP マッピングで使用されていない、D3DPTEXTURECAPS を設定する必要があります\_NONPOW2CONDITIONAL フラグ。

5.  デバイスには、テクスチャの次元が等しいか、のみサポートしているかどうかに設定する必要があります、 **dwTextureCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)格納する構造体、D3DPTEXTURECAPS\_SQUAREONLY フラグの適切なプリミティブ型 (線または三角形)。

デバイスは、最初と 2 番目の要件に記載されている以外の制限なしの任意のサイズのテクスチャをサポートする場合にする必要がありますしない設定の 4 番目と 5 番目の要件、サードパーティで説明されているフラグのいずれか。

### <a name="span-idtexturefilteringspanspan-idtexturefilteringspantexture-filtering"></a><span id="texture_filtering"></span><span id="TEXTURE_FILTERING"></span>テクスチャ フィルタ リング

拡大し、テクスチャを縮小するフィルターを有効になっているし、D3DTSS を通じて無効にする必要があります\_MAGFILTER と D3DTSS\_MINFILTER テクスチャ ステージの状態。 このフィルター処理する必要がありますできません。 自動的にこれらの状態が無効にするとします。 詳細については、D3DTSS\_*Xxx*テクスチャのステージの状態を Direct3D SDK ドキュメント D3DTEXTURESTAGESTATETYPE 列挙型を参照してください。

テクスチャが MIP マッピングを有効になっているし、D3DTSS を通じて無効にする必要があります\_MIPFILTER テクスチャ段階の状態。 この状態を無効にすると、テクスチャが MIP マップとして作成された場合は、デバイスは、MIP マップの最上位のレベルのみを使用する必要があります。 この状態が無効になっているときに、MIP マップのフィルター処理を実行しない必要があります。

値を使用して、最大異方性レベルをエクスポートする必要があります、デバイスは、異方性フィルタ リングをサポートする場合、 **dwMaxAnisotropy** (Direct3D SDK のドキュメントで定義されている) D3DDEVICEDESC7 構造体のメンバー。 さらに、デバイスが 1 から任意の設定を受け入れる必要があります**dwMaxAnisotropy** 、D3DTSS で\_MAXANISOTROPY テクスチャ段階の状態。

デバイスは、サポートされているすべてのフィルター モードをサポートされている任意の形式のテクスチャに適用できる必要があります。 たとえば、他のテクスチャ形式、MIP マッピングもサポートしている場合 YUV テクスチャの MIP マップをフィルター処理する必要がありますできるを実行します。

**注**   DirectX 9.0 と以降のアプリケーションで値を使用 D3DSAMPLERSTATETYPE 列挙サンプラーのレンダリングのテクスチャに関連する状態の特性を制御します。 DirectX 8.0 以降では、これらのサンプラーの状態が D3DTEXTURESTAGESTATETYPE 列挙に含まれます。 ランタイムは、ユーザー モード サンプラーの状態をマップ (D3DSAMP\_*Xxx*) には、カーネル モード D3DTSS\_*Xxx*値ドライバーがユーザー モード サンプラーの状態を処理する必要はありません。 D3DSAMPLERSTATETYPE の詳細については、DirectX SDK の最新のドキュメントを参照してください。

 

### <a name="span-ididirect3ddevice7validatedevicespanspan-ididirect3ddevice7validatedevicespanidirect3ddevice7validatedevice"></a><span id="idirect3ddevice7_validatedevice"></span><span id="IDIRECT3DDEVICE7_VALIDATEDEVICE"></span>IDirect3DDevice7::ValidateDevice

デバイスは、テクスチャ段階の状態にブレンド操作と、単一のパスでオペランドの特定の組み合わせをサポートしているかどうかは、デバイスは DD を返す必要があります\_への呼び出しには、[ok]、 **IDirect3DDevice7::ValidateDevice**メソッド (Direct3D SDK のドキュメントで説明) のようなそれぞれの組み合わせ。

返す必要がありますエラー コードのいずれかで使用できるかどうかは、デバイスが 1 つのパスでの操作をブレンド テクスチャ段階の状態の特定の組み合わせをサポートしていませんか描画操作またはオペランドの 1 つ以上をサポートしません、 **IDirect3DDevice7::ValidateDevice**メソッド。 無効な操作を描画できません通知なしに失敗、 **IDirect3DDevice7::ValidateDevice**メソッド。

 

 





