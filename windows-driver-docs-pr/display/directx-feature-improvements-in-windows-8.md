---
title: Windows 8 での DirectX 機能の向上
description: Windows 8 には、開発者、エンドユーザー、およびシステム製造元に役立つ Microsoft DirectX の機能強化が含まれています。
ms.assetid: 0622DA0D-41ED-4B47-B090-8D5B85E10EB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb1df9f714d02b0f85941cb068ac746904c83195
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838997"
---
# <a name="directx-feature-improvements-in-windows-8"></a>Windows 8 での DirectX 機能の向上


Windows 8 には、開発者、エンドユーザー、およびシステム製造元に役立つ Microsoft DirectX の機能強化が含まれています。

機能の改善点は次のとおりです。

-   [ピクセル形式 (5551、565、4444)](#pixelformats): 低電力のハードウェア構成で DirectX アプリケーションのパフォーマンスが向上します。
-   [倍精度シェーダーの機能](#dblshader): 高レベルシェーダーモデルのパフォーマンスが向上し、CPU を使用せずに GPU でさらに多くのことを行うことができます。
-   [ターゲットに依存しないラスタライズ](#tir): Direct2D アプリケーションの高パフォーマンスのアンチエイリアシングパス。
-   [[上書きと破棄なし](#noow)]: タイルベースのレンダラーを使用するモバイルプラットフォームおよび電源制約デバイスでの Microsoft Direct3D 11.1 アプリケーションのパフォーマンスが高くなります。
-   [すべてのステージでの Uavs](#uav): DirectX 11.1 ハードウェア上のすべてのシェーダーステージでシェーダーのデバッグを有効にする機能が追加されました。
-   [テクスチャ配列のプロセス間の共有 (ステレオスコピック3d をサポートするため)](#stereo): ステレオスコピック3-d を有効にするための基礎を提供します。
-   [複数サンプルのアンチエイリアスサンプルアクセスによる順序付けられていないアクセスビュー](#unordered): Direct3D 11 アプリケーションは、多数のサンプルにメモリを割り当てなくても、高品質のレンダリングアルゴリズムを実装できます。
-   [Logic ops](#logicops): 遅延シェーディング手法の機能強化。
-   [定数バッファーの制御が強化](#buffers)されました。ゲーム開発者のための効率的なバッファー管理です。

## <a name="span-idpixelformatsspanspan-idpixelformatsspanpixel-formats-5551-565-4444"></a><span id="pixelformats"></span><span id="PIXELFORMATS"></span>ピクセル形式 (5551、565、4444)


DirectX を使用した低電力構成でのグラフィックスのサポートを強化するには、Windows 8 用 Direct3D で、 [**DXGI\_FORMAT**](https://docs.microsoft.com/windows/desktop/api/dxgiformat/ne-dxgiformat-dxgi_format)列挙型の次の DirectX 9 ピクセル形式をサポートする必要があります。

-   **DXGI\_形式\_B5G6R5\_UNORM**
-   **DXGI\_形式\_B5G5R5A1\_UNORM**
-   **DXGI\_形式\_B4G4R4A4\_UNORM**

これらの追加の形式により、DirectX アプリケーションの低電力ハードウェアでのパフォーマンスが向上します。 これらの形式は、すべての Gpu でサポートされています。 次の表では、ハードウェアの機能レベルに応じて、これらの形式に必要なサポートについて説明します。

**ハードウェアの機能レベルに応じて必要な形式のサポート**

| 機能                       | 機能レベル 9\_x                                      | 機能レベル10.0                                             | 機能レベル10.1                        | 機能レベル 11 +                         |
|----------------------------------|---------------------------------------------------------|----------------------------------------------------------------|-------------------------------------------|-------------------------------------------|
| 型指定されたバッファー                     | X                                                      | 必須                                                       | 必須                                  | 必須                                  |
| 入力アセンブラー頂点バッファー    | X                                                      | 省略可能                                                       | 省略可能                                  | 省略可能                                  |
| Texture1D                        | X                                                      | 必須                                                       | 必須                                  | 必須                                  |
| Texture2D                        | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| Texture3D                        | X                                                      | 必須                                                       | 必須                                  | 必須                                  |
| TextureCube                      | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| シェーダー ld\*                      | X                                                      | 必須                                                       | 必須                                  | 必須                                  |
| シェーダーのサンプル\* (フィルター処理あり) | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| シェーダーの gather4                   | X                                                      | X                                                             | X                                        | 必須                                  |
| ミップマップ                           | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| Mipmap 自動生成           | 565では必須、4444では省略可能、5551               | 565では必須、4444では省略可能、5551                      | 565では必須、4444では省略可能、5551 | 565では必須、4444では省略可能、5551 |
| 作り                     | 565では必須、4444、5551の場合は no                     | 565では必須、4444では省略可能、5551                      | 565では必須、4444では省略可能、5551 | 565では必須、4444では省略可能、5551 |
| Blendable 作り           | 565では必須、4444、5551の場合は no                     | 565では必須、4444では省略可能、5551                      | 565では必須、4444では省略可能、5551 | 565では必須、4444では省略可能、5551 |
| UAV 型のストア                  | X                                                      | X                                                             | X                                        | 省略可能                                  |
| CPU のロック可能                     | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| 4x MSAA                          | 省略可能                                                | 省略可能                                                       | 565では必須、4444では省略可能、5551 | 565では必須、4444では省略可能、5551 |
| 8x MSAA                          | 省略可能                                                | 省略可能                                                       | 省略可能                                  | 565では必須、4444では省略可能、5551 |
| その他の MSAA サンプル数          | 省略可能                                                | 省略可能                                                       | 省略可能                                  | 省略可能                                  |
| マルチサンプリングの解決              | 565の必須 (MSAA がサポートされている場合)、4444の場合は5551 | 565の必須 (MSAA がサポートされている場合)、4444の場合は省略可能、5551  | 565では必須、4444では省略可能、5551 | 565では必須、4444では省略可能、5551 |
| マルチサンプリングの負荷                 | X                                                      | 565の必須 (MSAA がサポートされている場合)、4444の場合はオプション、5551の場合は省略可能 | 565では必須、4444では省略可能、5551 | 565では必須、4444では省略可能、5551 |

 

## <a name="span-iddblshaderspanspan-iddblshaderspandouble-precision-shader-functionality"></a><span id="dblshader"></span><span id="DBLSHADER"></span>倍精度シェーダーの機能


Windows 8 では、倍精度をサポートする Windows Display Driver Model (WDDM) 1.2 ドライバーは、すべてのシェーダーステージの高レベルシェーダーモデル5での追加の倍精度浮動小数点命令もサポートする必要があります。 手順は次のとおりです。

-   倍精度の逆数
-   倍精度の除算
-   倍精度のヒューズの乗算-加算

ランタイムはこれらの命令を直接ドライバーに渡すことができるため、実装では、パフォーマンスを最適化したり、ハードウェアで特別な手順として実装したりすることができます。

**注**   これらの機能を使用するには、開発者は、WDDM 1.2 以降のドライバーで倍精度サポート (D3D11\_機能\_double) を使用して、\_11 以上の機能\_レベルで実行されていることを確認する必要があります。

 

### <a name="span-idsum_of_absolute_differencesspanspan-idsum_of_absolute_differencesspanspan-idsum_of_absolute_differencesspansum-of-absolute-differences"></a><span id="Sum_of_absolute_differences"></span><span id="sum_of_absolute_differences"></span><span id="SUM_OF_ABSOLUTE_DIFFERENCES"></span>絶対差の合計

イメージ処理は、最新のデバイスで重要なアプリケーションです。 一般的な操作は、パターンマッチングまたは検索です。 ビデオエンコード操作では、通常、一致する四角形のタイル (通常は8x8 または 16x16) が検索されます。また、イメージ認識アルゴリズムでは、ビットマスクによって識別されるより一般的な図形が検索されます。 これらのシナリオのパフォーマンスを向上させるために、すべてのシェーダーステージのシェーダーモデル5.0 の Microsoft High Level Shader Language (HLSL) に新しい組み込みが追加されました。 この組み込み msad4 () はに対応し、シェーダー IL での絶対差分 (MSAD) 命令のマスクされた合計のグループを生成します。 すべての WDDM 1.2 以降のドライバーは、ハードウェアで直接、またはその他の指示 (エミュレートされたもの) として、この命令をサポートする必要があります。

**  、** ラップの動作ではなくオーバーフローが発生するように、msad 命令を実装することが理想的です。 オーバーフローの動作は未定義であることに注意してください。

この機能を使用するには、開発者が WDDM 1.2 以降のドライバーで機能\_レベル\_11 以降を使用して実行されていることを確認する必要があります。 開発者は、オーバーフローする (つまり、65535を超える) 累積値の結果精度に依存しないようにする必要があります。

 

## <a name="span-idtirspanspan-idtirspantarget-independent-rasterization-tir"></a><span id="tir"></span><span id="TIR"></span>ターゲットに依存しないラスタライズ (TIR)


ターゲットに依存しないラスタライズ (TIR) は、構造化されたグラフィックスの高品質のアンチエイリアシングを含む Direct2D 使用シナリオのための、ハイパフォーマンスのアンチエイリアシングパスを提供します。 TIR を使用すると、Direct2D は Direct2D アンチエイリアシングセマンティクスと品質を維持しながら、ラスターステップを CPU から GPU に移動できます。 この機能を使用すると、ソフトウェアレイヤーは多数のサブピクセルサンプル位置を評価しながら、少数のサンプルに必要なメモリのみを割り当てることができます。 これにより、GPU を使用して、CPU レンダリングされた実装のイメージの品質を維持するというパフォーマンス上の利点が得られます。 これにより、1つのサンプルを複数のサンプルのアンチエイリアスレンダリングターゲットの複数のサンプルにブロードキャストできます。

### <a name="span-idsamplecount__1__limited_tir_on_10__101___11_spanspan-idsamplecount__1__limited_tir_on_10__101___11_spanspan-idsamplecount__1__limited_tir_on_10__101___11_spansamplecount-1-limited-tir-on-10-101--11"></a><span id="SampleCount__1__Limited_TIR_on_10__10.1___11_"></span><span id="samplecount__1__limited_tir_on_10__10.1___11_"></span><span id="SAMPLECOUNT__1__LIMITED_TIR_ON_10__10.1___11_"></span>SampleCount = 1 (制限付き TIR、10.1 & 11)

Direct3D 10.0-Direct3D 11.0 ハードウェア (および機能レベル 10\_0-11\_0) では、ForcedSampleCount が 1 (およびレンダーターゲットビューのすべてのサンプル数) に設定され、記述された制限 (深度やステンシルなど) がサポートされます。

10\_0、10\_1、11\_0 ハードウェアの場合、 [**D3D11\_1\_DDI\_ラスタライザー\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1_ddi_rasterizer_desc)になります。**ForcedSampleCount**が1に設定されている場合、ラインレンダリングを2三角形 (四角形) ベースのモードに構成することはできません (つまり、 **multisampleenable**状態を true に設定することはできません)。 この制限は、11\_1 ハードウェアには存在しません。 **Multisampleenable**状態の名前付けは、マルチサンプリングを有効にする操作が不要になったため、誤解を招くことに注意してください。代わりに、線描画モードを選択するための、コントロールの1つである、またはその機能が**有効**になります。

この制限された形式のターゲット独立ラスタライズは、 **ForcedSampleCount** = 1 で、direct3d 10.0 に存在していたものの、direct3d 10.1 と direct3d (および機能レベル 10\_1 および 11\_0) では使用できなくなったため、使用できなくなりました。API の変更。 Direct3D 10.0 では、このモードは、 **multisampleenable**が false に設定されている場合に使用できる複数のサンプルのアンチエイリアシング (MSAA) 画面でも、中央からサンプリングされたレンダリングでした (これは、 **multisampleenable**を切り替えることによって切り替えることができます)。 Direct3D 10.1 以降では、 **Multisampleenable**は (名前にかかわらず) マルチサンプリングに影響しなくなり、ラインレンダリング動作のみを制御します。

## <a name="span-idnoowspanspan-idnoowspanno-overwrite-and-discard"></a><span id="noow"></span><span id="NOOW"></span>上書きも破棄もありません


### <a name="span-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanspan-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanspan-idrendering_content_on_a_tile-based_deferred-rendering__tbdr__architecturespanrendering-content-on-a-tile-based-deferred-rendering-tbdr-architecture"></a><span id="Rendering_content_on_a_tile-based_deferred-rendering__TBDR__architecture"></span><span id="rendering_content_on_a_tile-based_deferred-rendering__tbdr__architecture"></span><span id="RENDERING_CONTENT_ON_A_TILE-BASED_DEFERRED-RENDERING__TBDR__ARCHITECTURE"></span>タイルベースの遅延レンダリング (TBDR) アーキテクチャでのコンテンツのレンダリング

Direct3D 11.1 のレンダーターゲットは、新しいリソース Api のセットを使用して、破棄動作をサポートできるようになりました。 開発者は、この機能を認識し、TBDR アーキテクチャでより効率的に実行するために、追加の Discard () メソッドを呼び出す必要があります (従来のグラフィックスハードウェアにはペナルティがありません)。 これにより、モバイルプラットフォームや、タイル化されたレンダラーを使用するその他の電源制約デバイスのパフォーマンスが向上します。

### <a name="span-idupdating_resources_on_a_tbdr_architecturespanspan-idupdating_resources_on_a_tbdr_architecturespanspan-idupdating_resources_on_a_tbdr_architecturespanupdating-resources-on-a-tbdr-architecture"></a><span id="Updating_resources_on_a_TBDR_architecture"></span><span id="updating_resources_on_a_tbdr_architecture"></span><span id="UPDATING_RESOURCES_ON_A_TBDR_ARCHITECTURE"></span>TBDR アーキテクチャでのリソースの更新

TBDR アーキテクチャでは、同じコマンドバッファーに対して複数のパスが実行されるため、前の描画呼び出し中にサブリソースの一部が変更されていない場合は、特別な注意を払ってドライバーに通知する必要があります。 Direct3D**UpdateSubResource**関数で\_を上書きしないで使用すると、テクスチャの領域に対して以前の描画呼び出しが行われていないリソースを、ドライバーが管理するのに役立ちます。 これには、既存のデータを破棄するか、上書きから保護するかを、アプリケーションの目的をドライバーに通知する必要があります。 これにより、TBDR アーキテクチャでより効率的なレンダリングが可能になり、従来のデスクトップハードウェアで実行されてもペナルティは発生しません。

GPU 画面の一部を更新する Direct3D 11 UpdateSubresource () Api と CopySubresourceRegions Api の新しいバリエーションには、\_OVERWRITE または DISCARD を指定できない追加フラグフィールドが用意されています。

これらの Api は、Direct3D 11.1 device driver interface (DDI) と Direct3D 9 DDIs を駆動しています。 ここで説明するフラグを追加することで、変更された BLT、BUFBLT、VOLBLT、および TEXBLT DDIs をサポートするには、DirectX 9 + ハードウェア用の新しいドライバーが必要です。

これらは、Direct3D 11.1 ドライバーを使用するすべての Direct3D 10 + ハードウェアでもサポートされている必要があります。

## <a name="span-iduavspanspan-iduavspanuavs-at-every-stage"></a><span id="uav"></span><span id="UAV"></span>すべてのステージでの UAVs


Microsoft Direct3D 11 では、順序付けられていないアクセスビュー (UAVs) の数は、コンピューティングシェーダーでは8個に制限され、ピクセルシェーダーでは8個の結合 (レンダーターゲットビュー (RTVs) + UAVs) に制限されていました。 DirectX 11.1 では、バインドできる数が増加しています。 DirectCompute の場合、上限は64であり、グラフィックスの場合は、出力合併時の合計結合数が64になります (つまり、グラフィックには、RTVs で使用される可能性のある最大8を差し引いた64を含めることができます)。

順序指定されていないアクセスビューには、任意のシェーダーステージからアクセスできますが、グラフィックスパイプラインの合計は残ります。

すべてのシェーダーステージで UAVs を追加すると、パイプラインにデバッグ情報を追加できます。 この開発の容易さにより、Windows は、GPU 高速化アプリケーションを作成するためのより望ましいプラットフォームとなります。

これには、少なくとも DirectX 11.1 の機能レベルが必要です。

## <a name="span-idstereospanspan-idstereospancross-process-sharing-of-texture-arrays-for-supporting-stereoscopic-3-d"></a><span id="stereo"></span><span id="STEREO"></span>テクスチャ配列のプロセス間の共有 (ステレオスコピック3-d をサポートするため)


ステレオスコピック3-d はオプションの WDDM 1.2 システム機能ですが、ステレオスコピックのシステム機能をサポートするかどうかに関係なく、すべての WDDM 1.2 デバイスドライバーで実装する必要がある基になるインフラストラクチャがあります。

DirectX 10 (またはそれ以上) 対応のグラフィックスハードウェアでは、テクスチャ配列のプロセス間共有をサポートする必要があります。 この機能は、ステレオスコピック3-d を有効にするための基礎となります。 WDDM 1.2 Direct3D DDIs では、ハードウェアの機能レベルに依存しないレンダーターゲットとして、バッファー処理をサポートする必要があります。

この要件により、ステレオアプリケーションで mono モードでエラーが発生しないようにします。 たとえば、システムでステレオが有効になっていない場合でも、アプリケーションでは、レンダーターゲットとしてステレオスワップチェーンまたは格納バッファーを作成して、 **Present**を呼び出すことができます。 この場合は、左側のビューのみが表示されます (または、[*右*に Microsoft DirectX グラフィックスインフラストラクチャ (DXGI) が存在する] フラグが設定されていて、右側のビューのみ)。

そのため、WDDM 1.2 ドライバー (グラフィックス & レンダーデバイス) は、テクスチャ配列のクロスプロセス共有のサポートを追加することによって、Direct3D 11 Api をサポートする必要があります。 以前のバージョンでは、クロスプロセス共有リソースは単一層のサーフェイスである可能性がありました。 Windows 8 では、共有配列の最大サイズは2つの要素です (ステレオには十分です)。 この要件の詳細については、「Stereoscopic3DArraySupport [」を参照して](https://go.microsoft.com/fwlink/p/?linkid=324537)ください **。** その他の関連する Microsoft WindowsWindowsWindows HCK の要件は、 **ProcessingStereoscopicVideoContent**と**Stereoscopic3DModes**です。

## <a name="span-idunorderedspanspan-idunorderedspanuavs-with-multi-sample-anti-alias-sample-access"></a><span id="unordered"></span><span id="UNORDERED"></span>UAVs と複数サンプルのアンチエイリアスサンプルアクセス


Direct3D 11 では、レンダーターゲットビュー (RTVs)/DSVs にバインドされていない、順序付けられていないアクセスビュー (UAVs) に対してラスタライズを行うことができます。 UAVs は任意のサイズを持つことができますが、実装では、ビューポート/シザー四角形のピクセル寸法を使用してラスタライザーを操作できます。 DirectX 11 ハードウェアのサンプルパターンは、単一サンプルのみです。 DirectX 11.1 ハードウェア仕様が展開され、複数のサンプルを使用できるようになります。 これはターゲットに依存しないラスタライズの一種であり、UAVs のみが出力にバインドされています。

UAV-生成されるのは、ForcedSampleCount 状態から、サンプリングパターンが0、1、4、および8に制限されているサンプルパターン (TIR がサポートしている) を使用して、ラスタライザーでのマルチサンプリングのみです。 (UAVs 自体は、割り当てに関しては複数サンプリングされません)。0に設定すると、1単一のサンプルのラスタライズと同じになります。

シェーダーは、UAV のみのレンダリングでピクセル周波数の呼び出しを要求できます。 ただし、サンプルの頻度の呼び出しを要求することはできません (未定義の網掛け結果が生成されます)。 SampleMask ラスタライザーの状態は、ここではラスタライズの動作には影響しません。

この機能のサポートは DirectX 11.0 + ハードウェアで利用できます。これには、RTVs を使用したターゲットに依存しないラスタライズの全 11\_1 レベルをサポートしていないハードウェアも含まれます。 ドライバーは、UAV のみの複数サンプルのアンチエイリアスサンプルアクセス (MSAA) レンダリングをサポートしていることを報告できます (2 つのサンプルがサポートされています)。 すべての DirectX 11 + ハードウェアで1がサポートされます。 ハードウェアで、RTVs (16 サンプルサポートが必要) を使用して 11\_1 のターゲットに依存しないラスタライズを実行できる場合は、UAV のみの MSAA ラスタライズのサポートが必要です (つまり、UAV 専用のケースでは4と8のサンプル)。

この機能により、多数のサンプルにメモリを割り当てなくても、分析アンチエイリアシングなどの高品質のレンダリングアルゴリズムをアプリケーションで実装できるようになります。

## <a name="span-idlogicopsspanspan-idlogicopsspanlogic-operations"></a><span id="logicops"></span><span id="LOGICOPS"></span>ロジック操作


出力の合併時にロジック操作を可能にすると、現在不可能なイメージに対して何らかの操作を実行できます。 たとえば、マスクをより効率的に計算し、3-d レンダリング用の最新の遅延シェーディング手法を実装することもできます。

この機能は、ほとんどの3-d ハードウェアに存在しますが、現在のところ、色のブレンドは一般的ではありません。 その結果、logic ops の構成は次のように制限されます。

-   最初の RT blend desc で logic ops が使用されている場合、同じ logic op がすべての RTs に適用されるように、IndependentBlendEnable を false に設定する必要があります。
-   Logic ops を使用する場合、バインドされているすべての RenderTargets は UINT またはシント形式である必要があります。それ以外の場合、レンダリングは定義されていません。

## <a name="span-idbuffersspanspan-idbuffersspanimproved-control-of-constant-buffers"></a><span id="buffers"></span><span id="BUFFERS"></span>定数バッファーの制御の強化


### <a name="span-idpartialbufferspanspan-idpartialbufferspanpartial-constant-buffer-updates"></a><span id="partialbuffer"></span><span id="PARTIALBUFFER"></span>部分定数バッファーの更新

現在、定数バッファーでは、バッファー全体を上書きする更新中に、ソースからターゲットへのモノリシックコピーが必要です。 定数バッファーの一部だけを更新する必要がある場合は、書き込みのオフセットが理想的です。 このランダムアクセスを定数バッファーに書き込む機能は、ゲーム開発者によって要求され、自然で効率的なバッファー管理を実現します。 これらの機能は、他のバッファーの種類で既にサポートされており、WDDM 1.2 ドライバーの定数バッファーに追加されています。

この機能は、Direct3D 11.1 ドライバーを搭載したすべての Direct3D 10 + ハードウェアでサポートされている必要があります。 開発者にとっては、これは DirectX 9 ハードウェアでエミュレートされるので、すべての機能レベルで動作します。

**注**   上書きしない\_または破棄するフラグを指定する必要があります。

 

### <a name="span-idoffsetting_constant_buffer_updatesspanspan-idoffsetting_constant_buffer_updatesspanspan-idoffsetting_constant_buffer_updatesspanoffsetting-constant-buffer-updates"></a><span id="Offsetting_constant_buffer_updates"></span><span id="offsetting_constant_buffer_updates"></span><span id="OFFSETTING_CONSTANT_BUFFER_UPDATES"></span>オフセット (定数バッファーの更新を)

ハイパフォーマンスゲームエンジンを使用する場合の一般的な目的は、定数の定数バッファー更新の大規模なバッチを収集することです。これは、それぞれ独自の定数を必要とする個別の**描画\\** * 呼び出しによって参照されます。 これは、アプリケーションが大きなバッファーを作成し、その内部の領域に個々のシェーダーを示すことができるようにすることで容易になります (ビューに似ていますが、ビューを説明するためにオブジェクト全体を作成する必要はありません)。

個々のシェーダーでアドレス指定できる最大定数バッファーサイズを超えるサイズを持つ定数バッファーを作成できるようになりました (各要素の最大サイズは 4096 16 バイトで、各要素は 1 4、コンポーネントシェーダー定数)。 定数バッファーリソースのサイズは、システムが処理できるメモリ割り当てのサイズによってのみ制限されるようになりました。

4096要素を超える定数バッファーが、 **VSSetShaderConstants**などの **\*SetShaderConstants**api を使用してパイプラインにバインドされている場合は、サイズが4096要素だけであるかのようにシェーダーに表示されます。

**\*SetShaderConstants**api のバリアント **\*SetShaderConstants1**では、"Firstconstant" と "ConstantCount" をバインドと共に指定できます。 シェーダーは、このようにバインドされた定数バッファーにアクセスするときに、指定された "FirstConstant" オフセット (1 は16バイト) で開始したかのように見え、ConstantCount (16 バイト定数の数) によってサイズが定義されています。 これは基本的に、より大きな定数バッファーの領域の軽量な "ビュー" です。 (FirstConstant と ConstantCount はどちらも16の倍数である必要があります)。

この機能は、Direct3D 10 + ハードウェアのすべての WDDM 1.2 ドライバーでサポートされている必要があります。 Direct3D 11 ランタイムは、機能レベル 9\_x の適切な動作をエミュレートします。

## <a name="span-idclearviewspanspan-idclearviewspanclearview"></a><span id="clearview"></span><span id="CLEARVIEW"></span>Clearview


この機能により、実装は、1つの API/DDI 呼び出しで複数の rect をクリアすることで、ビデオメモリリソースに対して効率的な消去操作を実行できます。 この API には、消去するリソースのサブセットを定義する四角形のサポートが含まれています。 この機能は DirectX 9 DDI でサポートされており、Windows 8 ドライバー (WDDM 1.2) に必要です。 この方法では、イメージングや UI などで使用される2-d 操作のパフォーマンスが向上します。

## <a name="span-idcpyflagspanspan-idcpyflagspantileable-copy-flag"></a><span id="cpyflag"></span><span id="CPYFLAG"></span>タイル可能なコピーフラグ


タイル可能なコピー操作を使用すると、アプリケーションはイメージのソースと宛先がピクセル固定であることを実装に通知し、後続のレンダリングパスでは、クロスピクセルの情報交換には参加しません。 これにより、コピー操作中にイメージデータのサブセットをキャッシュすることによってメリットが得られる一部の実装では、パフォーマンスが大幅に向上します。 この機能は DirectX 9 DDI でサポートされており、Windows 8 以降のドライバー (WDDM 1.2) に必要です。

## <a name="span-idblitsspanspan-idblitsspansame-surface-blits"></a><span id="blits"></span><span id="BLITS"></span>同じ surface blits


スクロールなどの多くの UI 操作では、イメージのある部分から別の部分に画像データを転送する必要があります。 この機能により、コピー元の四角形と移動先の四角形の両方が同じイメージまたはリソース内にあるコピー操作のサポートが追加されます。 コピー元とコピー先の四角形が重なっている場合は、実装とドライバーによって状況が正しく処理される必要があります。 これは DirectX 9 DDI で既に必要であり、すべてのハードウェアの WDDM 1.2 で必要とされています。 この方法では、主要な UI シナリオのパフォーマンスが大幅に向上します。

## <a name="span-iddirect3d_111_ddispanspan-iddirect3d_111_ddispandirect3d-111-ddi"></a><span id="direct3d_11.1_ddi"></span><span id="DIRECT3D_11.1_DDI"></span>Direct3D 11.1 DDI


Windows 8 では、次の関数と構造が新しく追加または更新されています。

-   [*Debugbinary の割り当て*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_assigndebugbinary)
-   [*CalcPrivateBlendStateSize (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivateblendstatesize)
-   [*ClearView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_clearview)
-   [*DefaultConstantBufferUpdateSubresourceUP (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_resourceupdatesubresourceup)
-   [*ResourceUpdateSubresourceUP (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_resourceupdatesubresourceup)
-   [*VsSetConstantBuffers (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_setconstantbuffers)
-   [**D3D11\_1DDI\_D3D11\_オプション\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_d3d11_options_data)
-   [**D3DDDI\_BLTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_bltflags)
-   [**D3DDDI\_\_フラグをコピーする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_copy_flags)
-   [**D3DDDIARG\_BUFFERBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_bufferblt1)
-   [**D3DDDIARG\_破棄**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_discard)
-   [**D3DDDIARG\_TEXBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_texblt1)
-   [**D3DDDIARG\_VOLUMEBLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_volumeblt1)
-   [**D3DDDICAPS\_アーキテクチャ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicaps_architecture_info)
-   [**D3DDDICAPS\_SHADER\_MIN\_PRECISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddicaps_shader_min_precision)
-   [**D3DDDICAPS\_SHADER\_MIN\_PRECISION\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicaps_shader_min_precision_support)
-   [**D3DDDICAPS\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)

 

 





