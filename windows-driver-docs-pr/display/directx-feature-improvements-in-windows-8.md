---
title: Windows 8 での DirectX 機能の向上
description: Windows 8 には、開発者、エンドユーザーおよびシステムの製造元の利点を得られる Microsoft DirectX の機能強化が含まれています。
ms.assetid: 0622DA0D-41ED-4B47-B090-8D5B85E10EB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa4fb6c19989f24a30f5ced4630387a9474d3fad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328402"
---
# <a name="directx-feature-improvements-in-windows-8"></a>Windows 8 での DirectX 機能の向上


Windows 8 には、開発者、エンドユーザーおよびシステムの製造元の利点を得られる Microsoft DirectX の機能強化が含まれています。

次の領域には、機能の改善です。

-   [ピクセル形式 (5551、565、4444)](#pixelformats):低電力のハードウェア構成での DirectX アプリケーションのパフォーマンスを向上させる。
-   [倍精度シェーダー機能](#dblshader):さらに活用する高レベルのシェーダー モデル パフォーマンスの向上できる、CPU を使用することがなく GPU 上でします。
-   [ターゲットに依存しないラスタライズ](#tir):Direct2D アプリケーションの高パフォーマンスのアンチ エイリアス パス。
-   [上書きして破棄の欠如](#noow):モバイル プラットフォームとタイル ベース レンダラーを使用する power 制約デバイス上の Direct3D 11.1 の Microsoft アプリケーションのパフォーマンスを向上させる。
-   [すべてのステージにおいて UAVs](#uav):シェーダーの DirectX 11.1 ハードウェア上のすべてのシェーダー ステージでデバッグを有効にする機能を追加します。
-   [テクスチャ配列 (ステレオスコ ピック 3D をサポート) するためのプロセス間の共有](#stereo):ステレオスコ ピック 3-D が有効にするための基盤を提供します。
-   [順不同のマルチ サンプル アンチエイリアシング サンプルのアクセス権を持つアクセス ビュー](#unordered):サンプルの数が多い場合、メモリを割り当てられることがなく高品質な描画アルゴリズムを実装するために direct3d11 アプリケーションを有効にします。
-   [ロジックの ops](#logicops):遅延の網掛けの手法の改善。
-   [定数バッファーの制御を向上させる](#buffers):ゲーム開発者のための効率的なバッファー管理します。

## <a name="span-idpixelformatsspanspan-idpixelformatsspanpixel-formats-5551-565-4444"></a><span id="pixelformats"></span><span id="PIXELFORMATS"></span>ピクセル形式 (5551、565、4444)


DirectX を使用して低電力の構成でグラフィックスのサポート強化に、次の DirectX 9 ピクセルの形式から、 [ **DXGI\_形式**](https://msdn.microsoft.com/library/windows/desktop/bb173059)の Direct3D の列挙をサポートする必要がありますWindows 8 の場合:

-   **DXGI\_形式\_B5G6R5\_UNORM**
-   **DXGI\_形式\_B5G5R5A1\_UNORM**
-   **DXGI\_形式\_B4G4R4A4\_UNORM**

これらの追加の形式は、低電力ハードウェア DirectX アプリケーションでパフォーマンスの向上を提供します。 これらの形式は、累計のすべての Gpu でサポートされます。 このテーブルには、必要なハードウェアの機能レベルに応じて、これらの形式のサポートについて説明します。

**必要に応じてハードウェア機能レベルの形式のサポート**

| 機能                       | 機能レベル 9\_x                                      | 機能レベル 10.0                                             | 機能レベル 10.1                        | 機能レベル 11 以上                         |
|----------------------------------|---------------------------------------------------------|----------------------------------------------------------------|-------------------------------------------|-------------------------------------------|
| 型指定されたバッファー                     | X                                                      | 必須                                                       | 必須                                  | 必須                                  |
| 入力アセンブラー頂点バッファー    | X                                                      | 省略可能                                                       | 省略可能                                  | 省略可能                                  |
| Texture1D                        | X                                                      | 必須                                                       | 必須                                  | 必須                                  |
| Texture2D                        | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| Texture3D                        | X                                                      | 必須                                                       | 必須                                  | 必須                                  |
| TextureCube                      | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| シェーダー %ld\*                      | X                                                      | 必須                                                       | 必須                                  | 必須                                  |
| シェーダー サンプル\*(フィルター) を含む | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| シェーダー gather4                   | X                                                      | いいえ                                                             | X                                        | 必須                                  |
| Mipmap                           | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| Mipmap の自動生成           | 5551 必要な 565、4444、省略可能です。               | 5551 必要な 565、4444、省略可能です。                      | 5551 必要な 565、4444、省略可能です。 | 5551 必要な 565、4444、省略可能です。 |
| レンダリング ターゲット                     | 必要な 565、いいえ、4444 5551                     | 5551 必要な 565、4444、省略可能です。                      | 5551 必要な 565、4444、省略可能です。 | 5551 必要な 565、4444、省略可能です。 |
| Blendable レンダリング ターゲット           | 必要な 565、いいえ、4444 5551                     | 5551 必要な 565、4444、省略可能です。                      | 5551 必要な 565、4444、省略可能です。 | 5551 必要な 565、4444、省略可能です。 |
| UAV 型指定されたストア                  | X                                                      | いいえ                                                             | X                                        | 省略可能                                  |
| ロック可能な CPU                     | 必須                                                | 必須                                                       | 必須                                  | 必須                                  |
| 4 x MSAA                          | 省略可能                                                | 省略可能                                                       | 5551 必要な 565、4444、省略可能です。 | 5551 必要な 565、4444、省略可能です。 |
| 8 x MSAA                          | 省略可能                                                | 省略可能                                                       | 省略可能                                  | 5551 必要な 565、4444、省略可能です。 |
| その他の MSAA サンプル数          | 省略可能                                                | 省略可能                                                       | 省略可能                                  | 省略可能                                  |
| マルチ サンプリングの解決              | 必要な (MSAA がサポートされている) 場合、565 いいえ、4444 5551 | 565、4444、省略可能です (MSAA がサポートされている) 場合に必要な 5551  | 5551 必要な 565、4444、省略可能です。 | 5551 必要な 565、4444、省略可能です。 |
| マルチ サンプリング ロード                 | X                                                      | 565、4444、省略可能です (MSAA がサポートされている) 場合に必要な 5551) | 5551 必要な 565、4444、省略可能です。 | 5551 必要な 565、4444、省略可能です。 |

 

## <a name="span-iddblshaderspanspan-iddblshaderspandouble-precision-shader-functionality"></a><span id="dblshader"></span><span id="DBLSHADER"></span>倍精度シェーダー機能


Windows 8 で倍精度をサポートする Windows Display Driver Model (WDDM) 1.2 ドライバーは高レベルのシェーダー モデル 5 で、追加の倍精度浮動小数点命令をシェーダー ステージのすべてのもサポートする必要があります。 手順については、次のとおりです。

-   倍精度の逆数
-   倍精度の除算
-   倍精度に組み合わされ、乗算の追加します。

ランタイムは、ドライバーに直接これらの手順を渡すことのできるため、実装は、パフォーマンスを最適化または、ハードウェアで特殊化された 1 つの手順として実装できます。

**注**  開発者をこれらの機能を使用する機能を実行していることを確認する必要があります\_レベル\_11 以上の倍精度サポートと (D3D11\_機能\_DOUBLE) で、WDDM 1.2 またはそれ以降のドライバーです。

 

### <a name="span-idsumofabsolutedifferencesspanspan-idsumofabsolutedifferencesspanspan-idsumofabsolutedifferencesspansum-of-absolute-differences"></a><span id="Sum_of_absolute_differences"></span><span id="sum_of_absolute_differences"></span><span id="SUM_OF_ABSOLUTE_DIFFERENCES"></span>絶対差の合計

画像処理は、最新のデバイスで重要なアプリケーションです。 一般的な操作は、パターンに一致するか、検索です。 ビデオ エンコード操作は、通常、四角形のタイル (通常 8 x 8 または 16 x 16) の一致を検索し、イメージ認識アルゴリズムがビット マスクによって識別される一般的な図形を検索します。 このようなシナリオのパフォーマンスを向上させるために、新しい組み込みが追加されましたに、Microsoft 上位レベル シェーダー言語 (HLSL) Shader Model 5.0 のすべてのシェーダー ステージでします。 この組み込み msad4() に対応し、シェーダーの IL で絶対の相違点 (MSAD) 命令のマスク合計のグループが生成されます。 すべての WDDM 1.2 とそれ以降のドライバーは、ハードウェアで直接、またはその他の命令 (エミュレートされた) のセットとしてこの命令をサポートする必要があります。

**注**  理想的には、ラップの動作ではなくの飽和状態、そのオーバーフローが発生するように MSAD 命令を実装する必要があります。 オーバーフロー動作は定義されていないことに注意します。

開発者は、機能を実行していることを確認する必要があります\_レベル\_11 以降では、この機能を使用するには、WDDM 1.2 またはそれ以降のドライバーです。 開発者がオーバーフローする集積/離散値の精度を結果に依存する必要があります (つまり、65535 を超える参照してください)。

 

## <a name="span-idtirspanspan-idtirspantarget-independent-rasterization-tir"></a><span id="tir"></span><span id="TIR"></span>ターゲットに依存しないラスタライズ (TIR)


ターゲットに依存しないラスタライズ (TIR) は、構造化されたグラフィックスの高品質なアンチエイリアシングを含む Direct2D の使用状況シナリオの高パフォーマンスのアンチ エイリアス パスを提供します。 TIR、Direct2D のアンチエイリアシングのセマンティクスと品質を維持しながら、GPU に、CPU からラスタライズのステップに移動する Direct2D を使用できます。 この機能を使用して、ソフトウェア レイヤーは評価のカバレッジ、サブピクセル サンプル位置の数が多いまだのみ、少数のサンプルに必要なメモリを割り当てます。 これは、GPU を使用して表示するためには、CPU レンダリング実装のイメージ品質を維持したパフォーマンス上の利点を提供します。 これにより、複数のサンプルのマルチ サンプル アンチエイリアシングのレンダー ターゲットにブロードキャストする 1 つのサンプルです。

### <a name="span-idsamplecount1limitedtiron1010111spanspan-idsamplecount1limitedtiron1010111spanspan-idsamplecount1limitedtiron1010111spansamplecount-1-limited-tir-on-10-101--11"></a><span id="SampleCount__1__Limited_TIR_on_10__10.1___11_"></span><span id="samplecount__1__limited_tir_on_10__10.1___11_"></span><span id="SAMPLECOUNT__1__LIMITED_TIR_ON_10__10.1___11_"></span>SampleCount = 1 (10、10.1 & 11 限定 TIR)

Direct3D 10.0、11.0 の Direct3D ハードウェア (および機能レベル 10\_0 - 11\_0) ForcedSampleCount を 1 に設定をサポートしています (およびレンダリング ターゲット ビューのすべてのサンプル数) (たとえば、深さ/ステンシルなし) の制限事項が説明されているとします。

10 の\_0, 10\_1 から 11\_0 ハードウェア、 [ **D3D11\_1\_DDI\_ラスタライザー\_DESC**](https://msdn.microsoft.com/library/windows/hardware/hh451052).**ForcedSampleCount**設定されている (四角形) を 2 三角形を 1 に行のレンダリングを構成することはできません-ベースのモード (つまり、 **MultisampleEnable**状態を設定することはできませんを true に)。 この制限はない 11\_1 ハードウェア。 注意の名前を付け、 **MultisampleEnable**状態誤解を招くマルチ サンプリングを有効にするとはまったく関係がある不要になったためは、代わりは今すぐと共にコントロールの 1 つ**AntialiasedLineEnable**行レンダリング モードを選択するためです。

これで、ターゲットに依存しないラスターの形式を制限**ForcedSampleCount** = 1 は、近い Direct3D 10.0 に存在していたが、Direct3D 10.1 と Direct3D を使用できなくなったモード (および機能レベル 10\_1 から 11\_0) API が変更されたのためです。 Direct3D 10.0 では、このモードがあったときに使用可能な複数サンプル アンチ エイリアス (MSAA) 画面でも center サンプリング レンダリング**MultisampleEnable**を false に設定された (および切り替えることでこれを切り替えるでした**MultisampleEnable**)。 Direct3D の 10.1 以降、 **MultisampleEnable**不要になった (名前) に関係なく、マルチ サンプリングに影響し、行のレンダリング動作を制御するだけです。

## <a name="span-idnoowspanspan-idnoowspanno-overwrite-and-discard"></a><span id="noow"></span><span id="NOOW"></span>上書きして破棄の欠如


### <a name="span-idrenderingcontentonatile-baseddeferred-renderingtbdrarchitecturespanspan-idrenderingcontentonatile-baseddeferred-renderingtbdrarchitecturespanspan-idrenderingcontentonatile-baseddeferred-renderingtbdrarchitecturespanrendering-content-on-a-tile-based-deferred-rendering-tbdr-architecture"></a><span id="Rendering_content_on_a_tile-based_deferred-rendering__TBDR__architecture"></span><span id="rendering_content_on_a_tile-based_deferred-rendering__tbdr__architecture"></span><span id="RENDERING_CONTENT_ON_A_TILE-BASED_DEFERRED-RENDERING__TBDR__ARCHITECTURE"></span>遅延レンダリング (TBDR) タイルに基づくアーキテクチャ上のコンテンツのレンダリング

レンダー ターゲットで Direct3D 11.1 できるようになりました破棄動作リソース Api の新しいセットを使用しています。 開発者は、この機能に注意してくださいし、(従来のグラフィックス ハードウェアにペナルティがありません) を含む、TBDR アーキテクチャでより効率的に実行する追加の Discard() メソッドを呼び出す必要があります。 これにより、モバイル プラットフォームとタイルのレンダラーを使用するその他の電源の制約があるデバイス上のパフォーマンスが向上します。

### <a name="span-idupdatingresourcesonatbdrarchitecturespanspan-idupdatingresourcesonatbdrarchitecturespanspan-idupdatingresourcesonatbdrarchitecturespanupdating-resources-on-a-tbdr-architecture"></a><span id="Updating_resources_on_a_TBDR_architecture"></span><span id="updating_resources_on_a_tbdr_architecture"></span><span id="UPDATING_RESOURCES_ON_A_TBDR_ARCHITECTURE"></span>TBDR アーキテクチャ上のリソースを更新しています

TBDR アーキテクチャでは、同じコマンド バッファーに複数のパスを完了するためとサブ リソースの一部のドライバーが前の描画呼び出し中に変更されていないかを通知するのに特別な注意を使用する必要があります。 いいえを持つ\_上書きの使用率、Direct3D**UpdateSubResource**関数ドライバーが前の描画呼び出しが行われる場所なしテクスチャのリージョンにリソースを管理することができます。 これは、単に既存のデータを破棄または上書きから保護のいずれかのアプリケーションの目的のドライバーに通知することが必要です。 これは、TBDR アーキテクチャでのレンダリングを効率的に使用され、従来のデスクトップ ハードウェア上で実行した場合は、低下はありません。

いいえの場合、どちらも、GPU のサーフェイスの一部を更新するには、Direct3D 11 UpdateSubresource() や CopySubresourceRegions Api の変種は加算の Flags フィールドを提供する\_上書きまたは破棄を指定することができます。

これらの Api は、Direct3D 11.1 デバイス ドライバー インターフェイス (DDI) と Direct3D 9 Ddi ドライブします。 ここで説明するフラグを追加することで変更後の BLT、BUFBLT、VOLBLT、および TEXBLT Ddi をサポートするために、DirectX 9 + ハードウェア用の新しいドライバーが必要です。

これらはすべての Direct3D のサポートを必要とも 10 + Direct3D 11.1 ドライバーとハードウェア。

## <a name="span-iduavspanspan-iduavspanuavs-at-every-stage"></a><span id="uav"></span><span id="UAV"></span>すべてのステージにおいて UAVs


Microsoft direct3d11 で順序付けされておらずアクセス ビュー (UAVs) の数が 8 で計算シェーダーとを組み合わせた 8 に制限されています (レンダー ターゲット ビュー (RTVs) + UAVs)、ピクセル シェーダーにします。 DirectX 11.1、バインドできる数が引き上げられました。 DirectCompute はようになりました 64 に制限、グラフィックスの出力バインドされている合計合併は 64 (つまり、グラフィックスが、アップする-8 分の RTVs で使用される可能性がある-64)。

順序付けられていないアクセス ビューを任意のシェーダー ステージからアクセスできますが、まだグラフィックス パイプラインの合計から出て

UAVs を追加するすべてのシェーダー ステージ、パイプラインにデバッグ情報を追加することができます。 この使いやすさの開発は、GPU アクセラレータを使用したアプリケーションを記述するためのより適切なプラットフォームを Windows になります。

これには、少なくとも、DirectX 11.1 の機能レベルが必要です。

## <a name="span-idstereospanspan-idstereospancross-process-sharing-of-texture-arrays-for-supporting-stereoscopic-3-d"></a><span id="stereo"></span><span id="STEREO"></span>テクスチャ配列 (ステレオスコ ピック 3-D をサポート) するためのプロセス間の共有


ステレオスコ ピック 3-D は省略可能な WDDM 1.2 システムの機能は、基になるインフラストラクチャ ステレオスコ ピックの 3-D システムの機能をサポートするかどうかに関係なくすべての WDDM 1.2 デバイス ドライバによって実装する必要があります。

DirectX 10 (またはそれ以上)-対応のグラフィックス ハードウェアはテクスチャ配列のプロセス間の共有をサポートする必要があります。 この機能では、ステレオスコ ピック 3-D が有効にするための基盤を提供します。 WDDM 1.2 の Direct3D Ddi では、ハードウェアの機能レベルの独立したレンダー ターゲットとして配列バッファーのサポートが必要です。

この要件によって、ステレオのアプリケーションが mono のモードでの障害を必要はありません。 例: ケースの場合でもステレオが、システムで有効になっていないときにアプリケーション ステレオ スワップ チェーンを作成できる必要がありますまたはバッファーのレンダー ターゲットを呼び出して、配列化された**存在**します。 ここでは、左側のビューのみが表示されます (または、*右を好む* Microsoft DirectX Graphics Infrastructure (DXGI) 存在するフラグを設定すると、右側のビューのみ)。

したがって、WDDM 1.2 ドライバー (完全なグラフィックスおよびレンダリング デバイス) では、クロス テクスチャ配列のプロセスが共有のサポートを追加することで direct3d11 の Api をサポートする必要があります。 以前のバージョンでは、プロセス間の共有リソースにのみ単一レイヤー サーフェス可能性があります。 Windows 8 では、共有配列の最大サイズは 2 つの要素 (これは、ステレオ用だけで十分です) です。 この要件の詳細については、次を参照してください。 **Device.Graphics... Stereoscopic3DArraySupport**で[Windows ハードウェア認定要件](https://go.microsoft.com/fwlink/p/?linkid=324537)します。 関連するその他の Microsoft WindowsWindowsWindows HCK 要件は**Device.Graphics... ProcessingStereoscopicVideoContent**と**Device.Display.Monitor.Stereoscopic3DModes**します。

## <a name="span-idunorderedspanspan-idunorderedspanuavs-with-multi-sample-anti-alias-sample-access"></a><span id="unordered"></span><span id="UNORDERED"></span>アンチ エイリアス サンプルのマルチ サンプルのアクセス権を持つ UAVs


Direct3d11 にラスタライズ順不同でないレンダリング アクセス ビュー (UAVs) のターゲット ビュー (RTVs) により]、[Dsv にバインドします。 UAVs は、任意のサイズがあることができます、でも、実装は、ビューポートとシザリング四角形のピクセル寸法を使用して、ラスタライザーを操作できます。 DirectX 11 のハードウェアのサンプル パターンは、1 つのサンプルのみです。 複数のサンプルを許可する、DirectX 11.1 ハードウェア仕様を展開します。 これは、出力のバインドは UAVs のみのあるターゲットに依存しないラスタライズのバリエーションです。

ラスタライザーのマルチ サンプリングと共に UAV 専用のレンダリングとはキー 0、1、4、および 8 (16 ではない、TIR をサポートする) に限定サンプル パターンを使用した、ForcedSampleCount 状態オフで考えられるようになりました。 (UAVs 自体は、割り当ての観点からマルチ サンプリングされたできません)。0 の設定は、設定に相当 1 - 1 つのサンプルのラスタライズします。

シェーダーはピクセル頻度を呼び出すと UAV 専用のレンダリングを要求できます。 ただし、頻度のサンプル呼び出しの要求が無効です (未定義の網掛けの結果が生成されます)。 SampleMask ラスタライザーの状態では、ラスタライズ動作は、ここをまったく影響しません。

この機能は完全な 11 をサポートしていないハードウェアを含む DirectX 11.0 + ハードウェアの使用のサポート\_RTVs でターゲットに依存しないラスタライズの 1 レベル。 ドライバーが UAV 専用のマルチ サンプル アンチ エイリアス サンプルへのアクセス (MSAA) のレンダリングをサポートしていることを報告することができます (4 および 8 のサンプルを暗に示して両方サポートされます)。 DirectX 11 + のすべてのハードウェアには、1 がサポートしています。 ハードウェアが完全な 11 を実行できる場合\_(16 サンプルのサポートが必要です) が RTVs で 1 つのターゲットに依存しないラスタライズ UAV 専用の MSAA ラスタライズ サポートは (つまり UAV 専用の場合は、4 および 8 のサンプル) が必要です。

この機能は、多数のサンプルのメモリを割り当てられることがなく分析のアンチエイリアシングなどの高品質なレンダリング アルゴリズムを実装するためにアプリケーションを使用できます。

## <a name="span-idlogicopsspanspan-idlogicopsspanlogic-operations"></a><span id="logicops"></span><span id="LOGICOPS"></span>ロジックの操作


出力マージャーでロジック操作できるように現在は実現できないイメージでいくつかの操作を実行することができます。 たとえば、マスクをより効率的に計算し、また簡単には、3-D レンダリングの最新の遅延の網掛け手法を実装できます。

ほとんどの 3-D ハードウェアでこの機能が存在しますが、現在一般的な色のブレンドはことはできません。 その結果、ロジック ops の構成は、次の方法で制限します。

-   最初の RT blend desc で ops のロジックを使用している場合、同じロジック op がすべて RTs に適用されるよう IndependentBlendEnable は false に設定する必要があります。
-   Ops のロジックを使用している場合は、バインドされているすべての RenderTargets UINT またはシント ・の形式である必要があります、それ以外の場合、レンダリングは定義されていません。

## <a name="span-idbuffersspanspan-idbuffersspanimproved-control-of-constant-buffers"></a><span id="buffers"></span><span id="BUFFERS"></span>定数バッファーの制御を向上させる


### <a name="span-idpartialbufferspanspan-idpartialbufferspanpartial-constant-buffer-updates"></a><span id="partialbuffer"></span><span id="PARTIALBUFFER"></span>定数バッファーが部分的な更新プログラム

定数バッファーには、上書きバッファー全体の更新中にモノリシックのコピーをソースから変換先を今すぐ必要があります。 定数バッファーの一部のみを更新する必要があることが、場所の書き込みのオフセットは最適です。 定数バッファーに書き込み可能ランダム アクセスには、この機能は、ゲーム開発者によってが要求され、定数バッファー管理より自然で効率的です。 これらの機能は、他のバッファーの種類では、既にサポートされていましたし、WDDM 1.2 ドライバーの定数バッファーに追加されます。

この機能は、すべての Direct3D をサポートする必要があります 10 + Direct3D 11.1 ドライバーとハードウェア。 開発者にとって、これがエミュレートされる DirectX 9 ハードウェア上ですべての機能レベルで機能するためです。

**注**  か、なしを指定する必要があります\_上書きまたは破棄フラグ。

 

### <a name="span-idoffsettingconstantbufferupdatesspanspan-idoffsettingconstantbufferupdatesspanspan-idoffsettingconstantbufferupdatesspanoffsetting-constant-buffer-updates"></a><span id="Offsetting_constant_buffer_updates"></span><span id="offsetting_constant_buffer_updates"></span><span id="OFFSETTING_CONSTANT_BUFFER_UPDATES"></span>定数バッファーのオフセットの更新

高パフォーマンスのゲーム エンジンを希望は、定数バッファーを別に参照できる定数の更新の大きなバッチを収集する**描画\\***、各を必要とする独自の定数では、一度にすべてを呼び出します。 により、アプリケーションで大きなバッファーを作成して、その中のリージョンに個別のシェーダーをポイントし、これは容易になります (同様のビューには、ビューを記述する全体オブジェクトを作成する必要はありません)。

定数バッファー今すぐして作成できますをアドレス指定可能な定数バッファーの最大サイズよりも大きいサイズを持つ個々 のシェーダー (最大 4096 16 バイト要素 - 65 kB で、各要素は 1 つの 4 つの成分シェーダー定数です)。 定数バッファー リソースのサイズは、システムが処理できるメモリの割り当てのサイズによってのみ制限ようになりました。

使用して、パイプラインに 4096 要素より大きい定数バッファーがバインドされると **\*SetShaderConstants**ような Api **VSSetShaderConstants**、4096 のみがまるでシェーダーに表示されますサイズの要素。

バリアント、  **\*SetShaderConstants**Api、  **\*SetShaderConstants1**、バインドと一緒に指定するのには、"FirstConstant"と"ConstantCount"を使用します。 定数バッファー バインドされているこの方法では、表示されるかのように、指定された"FirstConstant"(1 は、16 バイト) オフセットから開始し、サイズがシェーダーへのアクセスを ConstantCount (16 バイトの定数の数) で定義されている場合は。 これは、基本的に、軽量の大きな定数バッファーの領域には、"View"です。 (両方 FirstConstant と ConstantCount あります 16 の倍数)。

この機能は、Direct3D の WDDM 1.2 のすべてのドライバーによってサポートされる必要があります 10 + ハードウェア。 Direct3d11 のランタイム機能レベルの 9 の適切な動作をエミュレートする\_x。

## <a name="span-idclearviewspanspan-idclearviewspanclearview"></a><span id="clearview"></span><span id="CLEARVIEW"></span>Clearview


この機能は、1 回の API/DDI 呼び出しで複数の四角形をオフにすると、ビデオ メモリ リソースの効率的なクリア操作を実行する実装を使用できます。 API には、削除するリソースのサブセットを定義する四角形のサポートが含まれています。 この機能は、DirectX 9 DDI でサポートされていたの Windows 8 のドライバー (WDDM 1.2) が必要です。 このアプローチの結果のイメージングで使用されるものなどの 2-d 操作のパフォーマンスを向上し、UI。

## <a name="span-idcpyflagspanspan-idcpyflagspantileable-copy-flag"></a><span id="cpyflag"></span><span id="CPYFLAG"></span>Tileable コピー フラグ


Tileable コピー操作では、イメージのソースと宛先のピクセルで配置し、後続のレンダリング パス内の情報の交換をクロス ピクセルに参加しません、実装に通知するアプリケーション。 これにより、コピー操作中にイメージ データのサブセットをキャッシュから利点を得られる一部の実装で大幅なパフォーマンスの向上。 この機能は、DirectX 9 DDI でサポートされていた、Windows 8 およびそれ以降のドライバー (WDDM 1.2) が必要です。

## <a name="span-idblitsspanspan-idblitsspansame-surface-blits"></a><span id="blits"></span><span id="BLITS"></span>同じ画面ブリット


スクロールなどの多くの UI 操作では、別のイメージの 1 つの部分からイメージ データを転送する必要があります。 この機能は、同じイメージまたはリソースの元の四角形と先の四角形の両方のコピー操作のサポートを追加します。 重複するソースと変換先の四角形の場合は、状況する必要がありますで処理される正しく実装とドライバー。 これは、DirectX 9 DDI で既に要求されたされ、すべてのハードウェアおよび WDDM 1.2 が必要があります。 このアプローチは、大幅なパフォーマンス向上の主要な UI シナリオで発生します。

## <a name="span-iddirect3d111ddispanspan-iddirect3d111ddispandirect3d-111-ddi"></a><span id="direct3d_11.1_ddi"></span><span id="DIRECT3D_11.1_DDI"></span>Direct3D 11.1 DDI


これらの関数と構造体は、新しい Windows 8 向けに更新されました。

-   [*AssignDebugBinary*](https://msdn.microsoft.com/library/windows/hardware/hh406234)
-   [*CalcPrivateBlendStateSize(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh406237)
-   [*ClearView*](https://msdn.microsoft.com/library/windows/hardware/hh406255)
-   [*DefaultConstantBufferUpdateSubresourceUP(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh802464)
-   [*ResourceUpdateSubresourceUP(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh439847)
-   [*VsSetConstantBuffers(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh439921)
-   [**D3D11\_1DDI\_D3D11\_オプション\_データ**](https://msdn.microsoft.com/library/windows/hardware/hh406442)
-   [**D3DDDI\_BLTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff544379)
-   [**D3DDDI\_コピー\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/hh451175)
-   [**D3DDDIARG\_BUFFERBLT1**](https://msdn.microsoft.com/library/windows/hardware/hh451069)
-   [**D3DDDIARG\_破棄**](https://msdn.microsoft.com/library/windows/hardware/hh451076)
-   [**D3DDDIARG\_TEXBLT1**](https://msdn.microsoft.com/library/windows/hardware/hh451142)
-   [**D3DDDIARG\_VOLUMEBLT1**](https://msdn.microsoft.com/library/windows/hardware/hh451145)
-   [**D3DDDICAPS\_アーキテクチャ\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451150)
-   [**D3DDDICAPS\_シェーダー\_MIN\_有効桁数**](https://msdn.microsoft.com/library/windows/hardware/hh451152)
-   [**D3DDDICAPS\_シェーダー\_MIN\_精度\_サポート**](https://msdn.microsoft.com/library/windows/hardware/hh451154)
-   [**D3DDDICAPS\_型**](https://msdn.microsoft.com/library/windows/hardware/ff544132)

 

 





