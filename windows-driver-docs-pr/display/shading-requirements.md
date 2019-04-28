---
title: シェーディング要件
description: シェーディング要件
ms.assetid: 6c4f3dee-a955-4140-8b64-e9289094f530
keywords:
- WDK Direct3D 網掛け
- フラット シェーディング WDK Direct3D
- グーロー シェーディング WDK Direct3D
- 反射ハイライトの WDK Direct3D
- アルファ ブレンディング WDK Direct3D
- ディザー WDK Windows 2000 の表示
- WDK Direct3D のカラー キー
- WDK Direct3D の透過性
- WDK Direct3D のブレンド
- WDK の Direct3D を強調表示
- D3DPRIMCAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5d4c8dfbcc11e7d0f6d8e1cd5cec489dcc8767a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382338"
---
# <a name="shading-requirements"></a>シェーディング要件


## <span id="ddk_shading_requirements_gg"></span><span id="DDK_SHADING_REQUIREMENTS_GG"></span>


フラットな影付き、グーロー シェーディング、鏡面ハイライト、アルファ ブレンドの要件、ディザリングとカラー キー次に示します。

### <a name="span-idflatshadingspanspan-idflatshadingspanflat-shading"></a><span id="flat_shading"></span><span id="FLAT_SHADING"></span>フラットな影付き

D3DPSHADECAPS\_COLORFLATRGB ビット、 **dwShadeCap**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)適切なプリミティブ型 (行の構造を設定する必要がありますまたは、三角形) フラット シェーディングがそのプリミティブ型のサポートされていることを指定するためにします。

三角形のファンを除くすべてのプリミティブ型、(サポートされている) 場合は、反射の色、およびアルファ データが、各プリミティブの最初の頂点から取得します。 三角形のファンの 2 番目の頂点が使用されます。 三角形全体にわたってこれらの色が変わらない (つまり、補間されません)。

### <a name="span-idgouraudshadingspanspan-idgouraudshadingspangouraud-shading"></a><span id="gouraud_shading"></span><span id="GOURAUD_SHADING"></span>グーロー シェーディング

**DwShadeCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)構造体の有効期限があります、D3DPSHADECAPS\_COLORGOURAUDRGB ビットが、適切なプリミティブ型 (の設定線または三角形) を色の補間をグーローがサポートされていることを示します。 色およびスペキュラ コンポーネントはどちらも線形補間しますの頂点の間。

すべてのプリミティブのカラー データは、プリミティブの頂点の間の線形補間を使用する必要があり、リファレンス ラスタライザーによって生成されたイメージに準拠している必要があります。 さらに、存在する場合は、すべてのカラーとアルファ コンポーネントを同じ方法で挿入する必要があります。 などフラット シェーディングをアルファ コンポーネントを使用しながら、RGB 色のコンポーネントのグーロー補間を使用することはできません。 例外の反射の色のアルファ コンポーネントを使用して、霧コンポーネントが送信されるべきではフラットな影が付きます。

繰り返し行う一連の色要素の奥行修正することをお勧めします。 Directx の最新のリリースでリファレンス ラスタライザーの色要素の奥行修正では既にに注意してください。 これは、現在のテスト手順でに考慮されます。

### <a name="span-idspecularhighlightingspanspan-idspecularhighlightingspanspecular-highlighting"></a><span id="specular_highlighting"></span><span id="SPECULAR_HIGHLIGHTING"></span>反射ハイライト

場合のサポートを強調表示が公開されていると後で、次のフラグの一方または両方を設定する必要があります、反射、 **dwShadeCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)用の構造、適切なプリミティブ型 (線または三角形):

-   D3DPSHADECAPS\_フラット シェーディングがサポートされている場合、SPECULARFLATRGB を設定する必要があります。

-   D3DPSHADECAPS\_グーロー シェーディングがサポートされている場合、SPECULARGOURAUDRGB を設定する必要があります。

また、これを有効にするか、D3DRENDERSTATE の適切な値を設定して、反射ハイライトを無効にすることがあります\_SPECULARENABLE が状態を表示します。

反射ハイライトと完全の色である必要があります、レンダー ターゲットを使用できる色の完全な範囲を生成できる必要があります。 単色の反射ハイライトはこの要件を満たすために十分ではありません。

D3DPSHADECAPS\_SPECULARFLATMONO と D3DPSHADECAPS\_SPECULARGOURAUDMONO フラグは単色の反射ハイライトを示すために使用されます。 のみを反射ハイライトが傾斜モードでサポートされていること示します。 アダプターが、rgb カラー モードでのみモノクロの反射の光源をサポートしているを示すことができるキャップはありません。 アダプターは、rgb カラー モードでのみモノクロの反射の光源をサポートする場合は、SPECULARFLATRGB または SPECULARGOURAUDRGB キャップを設定しないでください。 Monomodes で、ハードウェアは白の強度と反射コンポーネントの青のチャネルをだけ補する必要があります。 これは、D3DRENDERSTATE によって制御\_MONOENABLE が状態を表示します。

反射の光源を正しく実装するには、補間要素の 2 番目のセットが必要です。 ただし、ハードウェアはそのサポート z バッファーをパーツおよびブレンドできる多くの場合、エミュレート反射の光源 D3DCMP z の比較関数を使用した三角形の上に 2 番目の描画パスに設定することによって\_等しい (D3DCMPFUNC 列挙型を参照してください、DirectX SDK ドキュメント)。 この 2 番目のパスは、最初のパスの中に書き込まれたピクセルに補間の反射コンポーネントを追加する、blend に実行最大数を超える値は、白に飽和する必要があります。

### <a name="span-idalphablendingspanspan-idalphablendingspanalpha-blending"></a><span id="alpha_blending"></span><span id="ALPHA_BLENDING"></span>アルファ ブレンド

アルファ ブレンドのサポートを公開するで、次のフラグを設定、 **dwShadeCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)適切なプリミティブ型の構造型 (線または三角形):

-   D3DPSHADECAPS\_アルファとフラット シェーディングがサポートされている場合、ALPHAFLATBLEND を設定する必要があります。

-   D3DPSHADECAPS\_アルファとグーロー シェーディングがサポートされている場合、ALPHAGOURAUDBLEND を設定する必要があります。

アルファ ブレンドがサポートされている場合は、有効または、D3DRENDERSTATE の適切な値を設定して無効にする時間ができる必要があります\_ALPHABLENDENABLE が状態を表示します。

アルファ ブレンドの場合、または (3 D 空間) から完全な透過性は、受信の色をフレーム バッファーに既にあるデータの値で乗算のプロセスです。 このレンダリング状態が、D3DRENDERSTATE によって設定できるモード\_SRCBLEND と D3DRENDERSTATE\_DESTBLEND が状態を表示します。

描画操作のアルファ値が利用できない場合は、1.0 (不透明) と見なさ 必要があります。 これが可能な場合の例はアルファ チャネルがテクスチャをブレンドしません。

結果のピクセルの書き込み先となるターゲットにアルファ チャネルが含まれている場合は、透明度の適切な蓄積できるように、そのチャネルにアルファ ブレンディング操作の結果のアルファ値を書き込まれなければなりません。

### <a name="span-idditheringspanspan-idditheringspandithering"></a><span id="dithering"></span><span id="DITHERING"></span>ディザリング

特定のプリミティブ型 (線または三角形) にディザリングがサポートされている場合、 **dwRasterCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)構造体は、D3DPRASTERCAPS をいる必要があります\_ディザー フラグを設定します。 機能は、D3DRENDERSTATE によって制御可能である必要があります\_DITHERENABLE が状態を表示します。

ディザリングがサポートされている場合、可能性がありますを既定としないで常に off または常にします。

### <a name="span-idcolorkeyspanspan-idcolorkeyspancolor-key"></a><span id="color_key"></span><span id="COLOR_KEY"></span>カラー キー

カラー キーと関連するテクスチャの透明度、D3DPTEXTURECAPS\_透過性の上限 (を参照してください、 **dwTextureCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)構造体)。

カラー キー透明度の 2D スプライトの作成に使用されているオブジェクトの一部の色をフレーム バッファーにそれらの下にある色に置き換えます。 ドライバーが行えるように、シーン全体のカラー キーを有効にすることが - のカラー キー オンとオフをそれぞれの面にすることではなく添付のカラー キー値を持つ特定のサーフェスにだけ色キーを使用するアプリケーション。

場合に、・ カラーキーが有効になっている、D3DRENDERSTATE\_COLORKEYENABLE でレンダリング状態が に設定されている**TRUE**テクスチャ サーフェスであり、DDRAWISURF\_HASCKEYSRCBLT ビットが設定

場合に、カラー キーが有効になっている、D3DRENDERSTATE\_COLORKEYENABLE でレンダリング状態が に設定されている**TRUE**テクスチャ サーフェスであり、DDRAWISURF\_HASCKEYSRCBLT ビットが設定します。 (を参照してください、 **dwFlags**のメンバー、 [ **DD\_画面\_ローカル**](https://msdn.microsoft.com/library/windows/hardware/ff551733)詳細については、構造体)。アプリケーション作成 DDSD を使用するテクスチャ サーフェス\_CKSRCBLT を呼び出して、 **IDirect3DDevice7::SetRenderState** D3DRENDERSTATE メソッド\_COLORKEYENABLE と**TRUE**. これらの両方のカラー キーが発生する場合は true である必要があるあり、レンダリング状態のままにするアプリケーションを許可する必要があります**TRUE**すべて時間と引き続き選択的にフレームのテクスチャのサブセットを使用してカラー キー (が指定されている、DDRAWISURF\_HASCKEYSRCBLT ビットが設定)。 この動作を正しく処理するために、ドライバーの責任です。 詳細については**IDirect3DDevice7::SetRenderState**、Direct3D SDK のドキュメントを参照してください。

 

 





