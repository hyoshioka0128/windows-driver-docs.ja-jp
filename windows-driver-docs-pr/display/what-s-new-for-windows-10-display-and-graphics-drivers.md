---
title: Windows 10 ディスプレイおよびグラフィックス ドライバーの新機能
description: ディスプレイドライバー用の Windows 10 の新機能について説明します。
ms.assetid: 619175D4-98DA-4B17-8F6F-71B13A31374D
ms.date: 05/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 216bfce264256b623630892c85a67fc8fe39d509
ms.sourcegitcommit: d395d4b36f39d3557adda53735a4fdc8745a6408
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83666551"
---
# <a name="whats-new-for-windows-10-display-and-graphics-drivers"></a>Windows 10 ディスプレイおよびグラフィックス ドライバーの新機能

このページでは、Windows 10 バージョン 2004 (WDDM 2.7) のディスプレイとグラフィックスドライバーの新機能について説明します。 以前のバージョンの WDDM 2.x で追加された機能については、「[以前の wddm 2.x バージョンの新](what-s-new-for-prior-wddm-2-x-versions.md)機能」を参照してください。

## <a name="mesh-shaders"></a>メッシュシェーダー

メッシュシェーダーは、ラスタライズを使用するときに Direct3D 12 のグラフィックスパイプラインの柔軟性とパフォーマンスを向上させる手段です。 これらは入力アセンブラーの新しい置換として機能します。特に頂点およびジオメトリシェーダーのステージでは、入力アセンブラーの固定関数の動作の一部を柔軟な関数の動作に置き換えます。 メッシュシェーダーを使用すると、アプリケーションでは、入力アセンブラーよりも前に、より効率的にカリングを適用できます。 プリミティブは、GPU によって処理されるインデックスデータを持たずにカリングできます。これは、3D アプリケーションのプリミティブな数が時間の経過と共に増加するため、非常に便利です。

ピクセルシェーダーがアタッチされている場合、メッシュシェーダーからのプリミティブ出力は、ピクセルシェーダーステージに直接フィードされます。

メッシュシェーダー機能には、メッシュシェーダーステージと新しいステージ (増幅シェーダー) が導入されています。 Amplifications シェーダー GPU テセレーションステージを置き換えます。 アプリケーションでは、必要に応じてメッシュシェーダーを呼び出すように増幅シェーダーを設定します。 増幅シェーダーは省略可能な手順で、アプリケーションはジオメトリックの詳細レベルを動的に制御できます。

メッシュシェーダー機能には、新しいシェーディング言語構成要素と UMD 変更が含まれます。 メッシュシェーダーのレポートデバイス機能については、 [**D3D12DDI_D3D12_OPTIONS_DATA_0073**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_d3d12_options_data_0073)によって報告された**MeshShaderTier**というフィールドがあります。 また、2つの新しいシェーダーステージが導入されているため、 [**D3D12DDIARG_CREATE_PIPELINE_STATE_0075**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddiarg_create_pipeline_state_0075)、 **hMeshShader** 、 **hAmplificationShader**には2つの新しいフィールドがあります。 これを開始するには、コマンドリスト DDI [**PFND3D12DDI_DISPATCH_MESH_0074**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_dispatch_mesh_0074)を使用します。また、間接ディスパッチの[**D3D12DDI_INDIRECT_ARGUMENT_TYPE_DISPATCH_MESH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_indirect_argument_type)もあります。

## <a name="directx-raytracing-dxr-11"></a>DirectX Raytracing (DXR) 1.1

WDDM 2.7 では、Direct3D 12 の DXR の最初のリリースで構築されるいくつかの新機能と機能強化が導入されています。

- Inline raytracing は、独立したダイナミックシェーダーまたはシェーダーテーブルを使用しない別の形式の raytracing です。 これにより、開発者は、DXR 1.0 スタイルの raytracing を使用してシェーダーが "ダイナミックシェーダーベース" raytracing に適合しない場合に、柔軟性と利便性を高めることができます。 インライン raytracing は、計算シェーダー、ピクセルシェーダーなど、任意のシェーダーステージで使用できます。 これは、WDDM 2.7 で利用可能なものとして記載されていますが、DDI の変更に対応していません。

- アプリケーションは、ExecuteIndirect を通じて DispatchRays を呼び出すことができます。これにより、raytracing の作業を GPU で構成できるようになります。 これは、raytracing 作業のカリング、並べ替え、または調整をシークし、そのためにシェーダーを使用するアプリケーションに役立ちます。 これに加えて、D3D12DDI_INDIRECT_ARGUMENT_TYPE 列挙値が存在するようになりました。 間接 raytracing ディスパッチを使用する場合、実行間接バッファーの各要素の型は[**D3D12DDIARG_DISPATCH_RAYS_0054**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddiarg_dispatch_rays_0054)です。

- さまざまなシェーダーの組み合わせに対応するためにパイプラインの状態を作成するオーバーヘッドは、3D コンピューターのグラフィックスで発生する困難な問題の1つです。 DXR 1.1 には、オブジェクトの追加に役立つものが含まれています。 AddToStateObject () は API で公開されているため、アプリケーションは、追加されているものだけに比例して CPU オーバーヘッドを伴う既存の状態オブジェクトにシェーダーを追加できます。 これに加えて、 [**PFND3D12DDI_ADD_TO_STATE_OBJECT_0072**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_add_to_state_object_0072)と PFND3D12DDI_CALC_PRIVATE_ADD_TO_STATE_OBJECT_SIZE_0072 * *] () という2つのデバイス DDI 機能があり https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_calc_private_add_to_state_object_size_0072) ます。

一般的な機能レポートには、レポート層1.1 に使用[**D3D12DDI_RAYTRACING_TIER_1_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_raytracing_tier)新しい列挙値があります。

## <a name="sampler-feedback"></a>サンプラーのフィードバック

サンプラーのフィードバックは、テクスチャサンプリングの情報と場所をキャプチャして記録するための Direct3D 12 の機能です。 サンプラーのフィードバックがないと、これらの詳細は開発者にとって非透過的になります。 この機能により、アプリケーションは、どの mip がサンプリングされたかを知ることができますが、mips の場所を知ることができます。 アプリケーションでは、たとえば次のように、サンプリング情報に関心がある場合があります。

- テクスチャストリーミングシステムの次に読み込む内容を正確に把握します。
- テクスチャ空間シェーディングのレンダリングシステムに影を設定する必要があるものを正確に把握します。

サンプル操作のフィードバックは、inspectable 情報を取得するためにトランスコードする必要がある、不透明なリソースの一種として機能する "フィードバックマップ" に記述されています。フィードバック自体の作成と同様に、シェーダーモデル65には HLSL コンストラクトがあります。 セマンティクスは、Texture2D's サンプルとそのバリアントのセマンティクスによく似ています。

サンプラーのフィードバックでは新しいシェーディング言語の構造をよく使用しますが、UMD の変更も伴います。 デバイス機能チェックの場合、 [**D3D12DDI_D3D12_OPTIONS_DATA_0073**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_d3d12_options_data_0073)によって報告された SamplerFeedbackTier という cap があります。 リソースの作成が変更され、 [**D3D12DDI_MIP_REGION_0075**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_mip_region_0075)種類のサンプラーフィードバック mip 領域という新しいフィールドが作成されました。 これに加えて、新しい記述子作成メソッド[**PFND3D12DDI_CREATE_SAMPLER_FEEDBACK_UNORDERED_ACCESS_VIEW_0075**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_create_sampler_feedback_unordered_access_view_0075)もあります。

## <a name="content-protection"></a>Content Protection

オプションで保護されたリソースのサポートは、WDDM 2.7 の Direct3D 12 のビデオ操作に追加されました。 バックグラウンドでは、保護されたリソースは WDDM 2.7 より前に存在していましたが、ビデオではなく、API を使用した共有とグラフィックまたはコンピューティングでのみ利用できました。

保護されたリソースのサポートは、ドライバーによってグローバルなものとして報告されません。操作ごとに実行されます。 ドライバーが、特定の操作で保護されたリソースをサポートしていることを報告した場合、これは、その操作で保護されたリソースの読み取りと書き込みが可能であり、リソースの種類で使用できる場合は、クロス API 共有をサポートすることを意味します。 また、ドライバーが保護されたリソースを特定の形式でサポートする場合は、保護されていないリソースとしてもその形式をサポートする必要があることに注意してください。

WDDM 2.7 では、オプションの D3D12DDI_HPROTECTEDRESOURCESESSION インスタンスを取得するようにリソース作成メソッドが変更されます。 ドライバーは、セットアップと割り当てに通知するために、オブジェクト作成時にこのパラメーターを指定します。 さらに、操作で保護されたリソースを使用するかどうかを示すために、メモリの予算チェックが変更されます。 保護されたリソースセッションパラメーターが NULL 以外の場合、この操作によって保護されたリソースに書き込みが行われることを示します。 保護されていないリソースに書き込むには、operation オブジェクトを再作成する必要があります。

出力が保護されたリソースの場合、デコーダーおよびモーション推定参照は、保護されたリソースである必要があります。 保護されたリソースへの書き込み時に、保護されたリソースと保護されていないリソースの組み合わせからビデオ処理を読み取ることができます。

保護されたリソースに書き込む1つ以上の操作を記録する前に、NULL 以外の保護されたリソースセッションを使用して[**PFND3D12DDI_SETPROTECTEDRESOURCESESSION_0030**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_setprotectedresourcesession_0030)を呼び出す必要があります。 保護されていないリソースに書き込む1つ以上の操作を記録する前に、NULL を指定した**PFND3D12DDI_SETPROTECTEDRESOURCESESSION_0030**を呼び出す必要があります。

WDDM 2.7 でのコンテンツ保護の DDI 変更に関する上記のガイドツアー以外の詳細については、開始点としての[**D3D12DDI_VIDEO_DECODE_PROTECTED_RESOURCES_DATA_0072**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_video_decode_protected_resources_data_0072)を参照してください。

## <a name="improved-history-buffer-reporting-for-tools"></a>ツールの履歴バッファーレポートの向上

WDDM 2.7 では、GPU デバッグツールによる履歴バッファーの使用にメリットをもたらす DDI の変更が導入されています。 この変更により、1つのコマンドバッファーの送信には、一度に1つのコマンドリストではなく、複数のコマンドリストに対応する作業を含めることができます。 この変更により、GPU デバッグツールはアプリケーションのパフォーマンス特性をより正確に報告できます。

この機能は D3D12DDICAPS_TYPE_0073_SUPPORT_BATCHED_MARKERS によって報告されます。 列挙値 D3DDDIMLT_BATCHED の新しい[**D3DDDI_MARKERLOGTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_markerlogtype)があります。これは[**D3DDDI_BATCHEDMARKERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_batchedmarkerdata)に対応しています。 ETW イベントデータ構造体は、D3DDDIMLT_BATCHED 型の**D3DDDI_BATCHEDMARKERDATA**要素をいくつか含めるように revved されています。

## <a name="displayport-dp-auxi2c"></a>DisplayPort (DP) AUX/I2C

Dp 補助 (AUX) チャネルは、dp 構成データ (CD) へのアクセスを提供します。これは、DP デバイスの機能の読み取り、リンクトレーニング、トポロジ検出、I2C バスアクセスなどに使用される、デバイスごとの登録ファイルです。 開始点としての[DXGK_DP_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-dxgk_dp_interface)を参照してください。
