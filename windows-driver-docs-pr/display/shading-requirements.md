---
title: シェーディング要件
description: シェーディング要件
ms.assetid: 6c4f3dee-a955-4140-8b64-e9289094f530
keywords:
- シェーディング (WDK Direct3D)
- フラットシェーディング WDK Direct3D
- グーローシェーディング WDK Direct3D
- WDK 光源の強調表示 (WDK Direct3D)
- アルファブレンド WDK Direct3D
- WDK Windows 2000 ディスプレイのディザリング
- カラーキー WDK Direct3D
- 透過性 WDK Direct3D
- WDK Direct3D のブレンド
- WDK Direct3D の強調表示
- D3DPRIMCAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0678a0e7f7e8f6e608ee398caa2220965025d6a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825730"
---
# <a name="shading-requirements"></a>シェーディング要件


## <span id="ddk_shading_requirements_gg"></span><span id="DDK_SHADING_REQUIREMENTS_GG"></span>


フラットシェーディング、グーローシェーディング、反射の強調表示、アルファブレンド、ディザリング、およびカラーキーの要件は次のとおりです。

### <a name="span-idflat_shadingspanspan-idflat_shadingspanflat-shading"></a><span id="flat_shading"></span><span id="FLAT_SHADING"></span>フラットシェーディング

このプリミティブ型でフラットシェーディングがサポートされていることを示すために、 [**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**DWSHADECAP**メンバーの D3DPSHADECAPS\_COLORFLATRGB ビットを適切なプリミティブ型 (線または三角形) に対して設定する必要があります。

トライアングルファン以外のすべてのプリミティブ型では、色、スペキュラ (サポートされている場合)、およびアルファデータは、各プリミティブの最初の頂点から取得されます。 トライアングルファンの場合は、2番目の頂点が使用されます。 これらの色は、三角形全体にわたって一定のままです (つまり、補間されていません)。

### <a name="span-idgouraud_shadingspanspan-idgouraud_shadingspangouraud-shading"></a><span id="gouraud_shading"></span><span id="GOURAUD_SHADING"></span>グーローシェーディング

[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**dwShadeCaps**メンバーには、色のグーロー補間がサポートされることを示すために、適切なプリミティブ型 (線または三角形) に対して D3DPSHADECAPS\_COLORGOURAUDRGB ビットが設定されている必要があります。 色と反射のコンポーネントは、両方とも頂点間で直線的に補間されます。

すべてのプリミティブについて、カラーデータはプリミティブの頂点間の線形補間を使用する必要があり、参照ラスタライザーによって生成されたイメージに準拠している必要があります。 さらに、すべてのカラーおよびアルファコンポーネントが存在する場合は、同じ方法で補間する必要があります。 たとえば、アルファコンポーネントにはフラットシェーディングを使用しながら、色の RGB コンポーネントのグーロー補間を使用することは無効です。 例外として、反射色のアルファ成分を使用したフォグコンポーネントの送信があります。これは、フラットな影付きにすることはできません。

反復するカラーコンポーネントのパースペクティブ修正をお勧めします。 最新の Direct X リリースの参照ラスタライザーは、既に色コンポーネントのパースペクティブ修正を行っていることに注意してください。 これは、現在のテスト手順で考慮されます。

### <a name="span-idspecular_highlightingspanspan-idspecular_highlightingspanspecular-highlighting"></a><span id="specular_highlighting"></span><span id="SPECULAR_HIGHLIGHTING"></span>反射の強調表示

反射の強調表示のサポートが公開されている場合は、次のフラグのいずれかまたは両方を、適切なプリミティブ型 (線または三角形) の[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**dwShadeCaps**メンバーに設定する必要があります。

-   フラットシェーディングがサポートされている場合は、D3DPSHADECAPS\_SPECULARFLATRGB を設定する必要があります。

-   D3DPSHADECAPS\_SPECULARGOURAUDRGB は、グーローシェーディングがサポートされている場合に設定する必要があります。

また、D3DRENDERSTATE\_SPECULARENABLE レンダー状態の適切な値を設定して、反射の強調表示を有効または無効にすることもできます。

反射の強調表示は、完全な色である必要があり、レンダーターゲットで使用可能なすべての色を生成できる必要があります。 この要件を満たすには、モノクロの反射の強調表示は不十分です。

D3DPSHADECAPS\_SPECULARFLATMONO および D3DPSHADECAPS\_SPECULARGOURAUDMONO フラグは、グレーの反射の強調表示を示すためには使用されません。 これは、反射の強調表示がランプモードでサポートされていることのみを示します。 アダプターが RGB モードでの単色の反射の光源のみをサポートしていることを示すキャップはありません。 アダプターが RGB モードでモノクロ反射のハイライトのみをサポートしている場合は、SPECULARFLATRGB または SPECULARGOURAUDRGB のキャップを設定しないでください。 モノモードでは、ハードウェアはスペキュラコンポーネントの青チャネルを白の輝度として補間します。 これは、D3DRENDERSTATE\_モノ ENABLE レンダー状態によって制御されます。

反射の光源を適切に実装するには、interpolants の2番目のセットが必要です。 ただし、z バッファリングとブレンドをサポートするハードウェアパートでは、多くの場合、三角形に対して2番目のブレンドパスを使用することによって、反射の光源をエミュレートできます (D3DCMP\_等しいとして設定します (DirectX SDK の D3DCMPFUNC 列挙型を参照してください)。ドキュメント)。 この2番目のパスでは、blend を実行して、最初のパス中に書き込まれたピクセルに補間反射成分を追加します。最大値を超える値は、白に飽和する必要があります。

### <a name="span-idalpha_blendingspanspan-idalpha_blendingspanalpha-blending"></a><span id="alpha_blending"></span><span id="ALPHA_BLENDING"></span>アルファブレンド

アルファブレンドのサポートを公開するには、次のフラグを適切なプリミティブ型 (線または三角形) の[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**dwShadeCaps**メンバーに設定する必要があります。

-   D3DPSHADECAPS\_ALPHAFLATBLEND は、アルファでフラットシェーディングがサポートされている場合に設定する必要があります。

-   D3DPSHADECAPS\_ALPHAGOURAUDBLEND は、アルファでグーローシェーディングがサポートされている場合に設定する必要があります。

アルファブレンドがサポートされている場合は、D3DRENDERSTATE\_ALPHABLENDENABLE render 状態の適切な値を設定することによって、それを有効または無効にできる必要があります。

アルファブレンド (3D 空間からの真の透明度) は、フレームバッファーに既に配置されているデータの値によって入力色を modulating するプロセスです。 このレンダリング状態には、D3DRENDERSTATE\_SRCBLEND および D3DRENDERSTATE\_DESTBLEND レンダリング状態で設定できるモードがあります。

ブレンド操作のアルファ値を使用できない場合は、1.0 (不透明) であると想定する必要があります。 これが可能な場合の例として、アルファチャネルを持たないテクスチャとのブレンドがあります。

結果のピクセルが書き込まれるターゲットにアルファチャネルが含まれている場合は、アルファブレンディング演算の結果として得られるアルファ値をそのチャネルに書き込む必要があります。これにより、透明度を適切に累積できます。

### <a name="span-idditheringspanspan-idditheringspandithering"></a><span id="dithering"></span><span id="DITHERING"></span>ディザリング

特定のプリミティブ型 (線または三角形) でディザリングがサポートされている場合、 [**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**dwRasterCaps**メンバーには、D3DPRASTERCAPS\_のディザーフラグが設定されている必要があります。 この機能は、D3DRENDERSTATE\_DI[ENABLE render state] を使用して制御可能である必要があります。

ディザリングがサポートされている場合、既定では [オフ] または [常時オン] にならないことがあります。

### <a name="span-idcolor_keyspanspan-idcolor_keyspancolor-key"></a><span id="color_key"></span><span id="COLOR_KEY"></span>色キー

カラーキーは、テクスチャの透明度と D3DPTEXTURECAPS\_透明度キャップ ( [**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**Dwtexturecaps**メンバーを参照) に関連しています。

カラーキーの透過性は、2D スプライトを作成するために使用され、オブジェクトの一部の色を、フレームバッファー内でその下にある色に置き換えます。 このドライバーを使用すると、アプリケーションでシーン全体のカラーキーを有効にすることができますが、各画面でカラーキーをオンまたはオフにするのではなく、接続されたカラーキー値を持つ特定のサーフェイスに対してのみカラーキーを使用する必要があります。

D3DRENDERSTATE\_COLORKEYENABLE レンダー状態が**TRUE**に設定され、テクスチャサーフェイスに DDRAWISURF\_HASCKEYSRCBLT ビットセットがある場合は、colorkeyが有効になります。

D3DRENDERSTATE\_COLORKEYENABLE レンダー状態が**TRUE**に設定され、テクスチャサーフェイスに DDRAWISURF\_HASCKEYSRCBLT ビットが設定されている場合、カラーキーが有効になります。 (詳細については、 [**DD\_SURFACE\_ローカル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)構造の**dwFlags**メンバーを参照してください)。アプリケーションでは、DDSD\_CKSRCBLT を使用するテクスチャサーフェイスを作成し、D3DRENDERSTATE\_COLORKEYENABLE および**TRUE**を使用して**IDirect3DDevice7:: SetRenderState**メソッドを呼び出します。 これらはどちらも、カラーキーを使用するには true である必要があります。また、アプリケーションでは、レンダリング状態を常に**true**のままにしておき、フレームのテクスチャのサブセット (つまり、\_DDRAWISURF を持つもの) に対してカラーキーを選択的に使用することが許可されている必要があります。HASCKEYSRCBLT ビットセット)。 この動作を正しく処理するには、ドライバーが必要です。 **IDirect3DDevice7:: SetRenderState**の詳細については、Direct3D SDK のドキュメントを参照してください。

 

 





