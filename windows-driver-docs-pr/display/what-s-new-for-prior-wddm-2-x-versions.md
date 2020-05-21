---
title: 以前の WDDM 2.x バージョンで追加された機能
description: ディスプレイドライバーとグラフィックスドライバーの以前の Windows 10 リリースでの機能について説明します。
ms.assetid: 22793a7e-38fc-4cd8-aafd-09dfed48cb02
ms.date: 03/24/2020
ms.localizationpriority: medium
ms.custom: seodec18, 19H1
ms.openlocfilehash: f216dae793c91403b5b53685a59484fb76a09e31
ms.sourcegitcommit: d395d4b36f39d3557adda53735a4fdc8745a6408
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83666553"
---
# <a name="features-added-in-prior-wddm-2x-versions"></a>以前の WDDM 2.x バージョンで追加された機能

このページでは、以前のバージョンの Windows 10 用 WDDM 2.x で追加された、表示ドライバーとグラフィックスドライバーの機能について説明します。 最新の WDDM 2.x バージョン用に追加された新機能については、「 [Windows 10 のディスプレイドライバーとグラフィックスドライバーの新](what-s-new-for-windows-10-display-and-graphics-drivers.md)機能」を参照してください。

## <a name="wddm-26"></a>WDDM 2.6

### <a name="super-wet-ink"></a>スーパーウェットインク

*スーパーウェットインク*は、*フロントバッファーレンダリング*を中心とした機能です。 IHV ドライバーは、ハードウェアでサポートされていない形式またはモードの "表示可能な" テクスチャの作成をサポートできます。 これを行うには、アプリが要求したテクスチャと、表示可能な形式/レイアウトの "影" テクスチャを割り当てて、現在の2つの間でコピーします。 この "影" は、通常の方法ではテクスチャであるとは限りませんが、圧縮データのみになる可能性があります。 また、存在する必要がない場合もありますが、最適化されている可能性があります。

次のように、表示可能なサーフェイスのこれらの側面を理解するために、ランタイムが進化します。

* 特定の VidPnSource/平面での表示に影が存在する必要があるかどうか。

* シャドウが存在するかどうかを指定します。

* アプリケーション画面からシャドウサーフェイスにコンテンツを転送する場合。 ランタイムは、この操作について明示的に実行されますが、現在は暗黙的であるとは限りません。

* モードの設定を要求する方法、または元のサーフェスとシャドウサーフェスを動的に反転する方法。

Scanout は、VBlank の直後に開始され、イメージの上から下へスキャンされ、次の VBlank のすぐ前に完了します。 これは、ピクセルクロックのタイミングやテクスチャ内のデータのレイアウトによっては、常にそうであるとは限りません。特に、圧縮が実際に使用可能な場合。

スキャンを実行する前に発生する変換を個別に理解するために新しい DDIs を追加し、可能な場合は、フロントバッファーレンダリングを有効にします。 [D3DWDDM2_6DDI_SCANOUT_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm2_6ddi_scanout_flags) と [PFND3DWDDM2_6DDI_PREPARE_SCANOUT_TRANSFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_6ddi_prepare_scanout_transformation) を参照してください。

### <a name="variable-rate-shading"></a>変動率の網掛け

変動率の網かけ、または粗いピクセルの網掛けは、レンダリングされた画像全体にわたって、表示パフォーマンスと電力の割り当てをさまざまな速度で実現するためのメカニズムです。

前のモデルで、MSAA (複数のサンプルのアンチエイリアシング) を使用して幾何学的な別名を減らすには、次の手順を実行します。

* ターゲットが割り当てられているときに、幾何学的なエイリアスを減らすための量を事前に把握しておく必要があります。
* ターゲットが割り当てられると、幾何学的なエイリアシングを減らすための量を変更することはできません。

WDDM 2.6 では、新しいモデルは、*粗い網掛け*の新しい概念を追加することによって、MSAA を粒度の*粗いピクセル*方向に拡張します。 ここでは、網掛けをピクセルよりも粗い頻度で実行できます。 ピクセルのグループは1つの単位として網掛けでき、結果はグループ内のすべてのサンプルにブロードキャストされます。

粗いシェーディング API を使用すると、アプリは、網掛けされたグループに属するピクセル数を指定できます。 粗いピクセルサイズは、レンダーターゲットが割り当てられた後に変化する可能性があります。 そのため、画面のさまざまな部分や描画パスが異なると、コースの網掛け率が異なる場合があります。

多層実装は、2つのユーザークエリキャップで使用できます。 階層1および2では、1つのサンプリングリソースと MSAA リソースの両方に対して粗い網掛けを使用できます。 MSAA リソースの場合、シェーディングは、通常どおり、粗いピクセル単位またはサンプル単位で実行できます。 ただし、階層1および2では、MSAA リソースに対して、粒度の粗いサンプリングを使用して、ピクセルごととサンプルごとの頻度で網掛けを行うことはできません。

階層 1:

* 網掛け率は、描画単位でのみ指定できます。これよりも詳細なものはありません。

* シェード率は、レンダーターゲット内の場所とは無関係に描画されるものに一様に適用されます。  

階層 2:

* 網掛け率は、階層1のように、描画単位で指定できます。 また、描画ごとにとの組み合わせで指定することもできます。

  * Provoking からのセマンティック、および
  * Screenspace イメージ

* コンバイナーのセットを使用して3つのソースからの網掛け率が組み合わされます。
* 画面領域のイメージタイルのサイズは16x16 以下です。 アプリによって要求された網掛け率は、正確に配信されることが保証されています (テンポラルとその他の再構築フィルターの有効桁数)

* SV_ShadingRate PS 入力がサポートされています。 1つのビューポートが使用されていて、SV_ViewportIndex が書き込まれていない場合にのみ、provoking の頂点レートが有効になります。

* SupportsPerVertexShadingRateWithMultipleViewports cap が true とマークされている場合、provoking の頂点レートは、プリミティブごとのレートとも呼ばれ、複数のビューポートで使用できます。 また、その場合は、SV_ViewportIndex の書き込み時に使用することもできます。

[PFND3D12DDI_RS_SET_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_rs_set_shading_rate_0062) と [D3D12DDI_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_shading_rate_0062) を参照してください。

### <a name="collect-diagnostic-info"></a>診断情報の収集

*診断情報を収集*すると、OS はレンダリングと表示の両方の機能で構成されたグラフィックスアダプターのドライバーからプライベートデータを収集できます。 この新機能は、WDDM 2.6 の要件です。

新しい DDI では、ドライバーが読み込まれるたびに、OS が情報を収集できるようにする必要があります。 現時点では、OS は、ミニポートによって実装された DxgkDdiCollectDebugInfo 関数を使用して、TDR (タイムアウト検出と復旧) 関連のケースに対してドライバーのプライベートデータを照会します。 新しい DDI は、さまざまな理由でデータを収集するために使用されます。 OS は、要求された種類の情報を提供する診断が必要になったときに、この DDI を呼び出します。 ドライバーは、問題を調査して OS に送信するために重要なすべてのプライベート情報を収集する必要があります。 DxgkDdiCollectDebugInfo は、最終的には非推奨となり、DxgkDdiCollectDiagnosticInfo に置き換えられます。

[DXGKDDI_COLLECTDIAGNOSTICINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_collectdiagnosticinfo) を参照してください。

### <a name="background-processing"></a>バックグラウンド処理

バックグラウンド処理を使用すると、ユーザーモードドライバーは必要なスレッド動作を表現でき、ランタイムは制御/監視を行うことができます。 ユーザー モード ドライバーでは、バックグラウンド スレッドをスピンアップし、可能な限り低い優先度を割り当てます。また、これらのスレッドによってクリティカル パス スレッドが中断せず、全般的には成功するように NT スケジューラを利用します。

Api を使用すると、アプリは、ワークロードに適したバックグラウンド処理の量と、その作業を実行するタイミングを調整できます。

[PFND3D12DDI_QUEUEPROCESSINGWORK_CB_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_queueprocessingwork_cb_0062) を参照してください。

### <a name="driver-hot-update"></a>ドライバーのホットアップデート

ドライバーのホットアップデートでは、OS コンポーネントを更新する必要がある場合に備えて、サーバーのダウンタイムを削減できます。

ドライバーホットパッチは、カーネルモードドライバーにセキュリティ修正プログラムを適用するために使用されます。 この場合、ドライバーはアダプターのメモリを保存するように求められます。アダプターが停止し、ドライバーがアンロードされ、新しいドライバーが読み込まれ、アダプターが再起動されます。

[DXGKDDI_SAVEMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_savememoryforhotupdate)と[DXGKDDI_RESTOREMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restorememoryforhotupdate)を参照してください。

## <a name="wddm-25"></a>WDDM 2.5

### <a name="tracked-workloads"></a>追跡対象のワークロード

追跡されたワークロードは試験的な機能であり、より高速なプロセッサの実行と電力消費の削減の間のトレードオフをより細かく制御でき、さらに通知されるまでは利用できません。 実装は、Windows 10 バージョン2003から削除されました。また、以前のバージョンの OS からは、セキュリティ修正プログラムの一部として非推奨とされています。

### <a name="content-changes"></a>コンテンツの変更

| トピック | 日付 | 説明 |
| --- | --- | --- |
| [HMDs および特殊な表示用の EDID 拡張機能 (VSDB)](specialized-monitors-edid-extension.md) | 2018 年 12 月 3 日 | ディスプレイの製造元の仕様 |
| [DirectX グラフィックスカーネルサブシステム (Dxgkrnl)](directx-graphics-kernel-subsystem.md) | 12/04/2018 | Windows オペレーティングシステムが Microsoft DirectX グラフィックスカーネルサブシステム (Dxgkrnl) を介して実装するカーネルモードインターフェイス。 |
| [WDDM 2.1 の機能](wddm-2-1-features.md) | 01/10/2019|WDDM 2.1 の新機能と更新された機能について説明します。 |

### <a name="raytracing"></a>Raytracing

新しい Direct3D DDI は、ハードウェアアクセラレータの raytracing をサポートするために、Direct3D API と並行して作成されました。 次のような DDI があります。

* [PFND3D12DDI_BUILD_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_build_raytracing_acceleration_structure_0054)
* [PFND3D12DDI_COPY_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_copy_raytracing_acceleration_structure_0054)
* [PFND3D12DDI_EMIT_RAYTRACING_ACCELERATION_STRUCTURE_POSTBUILD_INFO_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_emit_raytracing_acceleration_structure_postbuild_info_0054)
* [PFND3D12DDI_GET_RAYTRACING_ACCELERATION_STRUCTURE_PREBUILD_INFO_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_get_raytracing_acceleration_structure_prebuild_info_0054)

Raytracing の詳細については、次の情報を参照してください。

* [Microsoft DirectX Raytracing の発表](https://devblogs.microsoft.com/directx/announcing-microsoft-directx-raytracing/)
* [DirectX Raytracing と Windows 10 10 月2018更新プログラム](https://devblogs.microsoft.com/directx/directx-raytracing-and-the-windows-10-october-2018-update/)
* [DirectX フォーラム](https://forums.directxtech.com/index.php?topic=5985.0)

### <a name="display-synchronization"></a>同期の表示

ディスプレイがドライバーによって OS に公開されている場合、OS はディスプレイの同期機能をチェックし、表示を有効にします。 TypeIntegratedDisplay 子デバイスの場合は、アダプターの初期化時に*型* [DXGKQAITYPE_INTEGRATED_DISPLAY_DESCRIPTOR2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)を持つ[DxgkDdiQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)を呼び出すことによって報告されます。 WDDM 2.5 以降でサポートされている TypeVideoOutput 子デバイスの場合、機能はターゲットまたは接続されたモニターに基づいて変更される可能性があるため、 [DxgkDdiUpdateMonitorLinkInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updatemonitorlinkinfo)を介してホットプラグ処理の一部として報告されます。

OS は、 [DxgkDdiSetTimingsFromVidPn](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)呼び出しで、パスごとの[DXGK_SET_TIMING_PATH_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_set_timing_path_info#input)構造の入力フィールドの表示同期を指定します。

## <a name="wddm-21"></a>WDDM 2.1

WDDM 2.1 を使用すると、新しいシナリオが可能になり、パフォーマンス、信頼性、アップグレードの回復性、診断の改善、および Windows グラフィックスサブシステムの将来のシステムの向上の領域が大幅に改善されます。
WDDM 2.0 ドライバーモデルは、D3D12 の前提条件です。 WDDM 2.0 および DirectX12 は、Windows 10 以降でのみ使用できます。

WDDM 2.1 の機能の追加と更新の一覧を次に示します。

* メモリ管理に費やされるオーバーヘッド時間を短縮し、大量のグラフィックスメモリをより効率的に使用することで、グラフィックスのパフォーマンスが向上しました。 グラフィックスパフォーマンスの向上は次のとおりです。

  * リソースの提供と回収-バックグラウンドモードで実行されているアプリケーションのメモリフットプリントを削減するための機能強化を提供し、再利用できます。
  * 2 MB のページテーブルエントリエンコーディングのサポート-WDDM 2.1 では、VRAM の大きなページテーブルエントリ (PTE) エンコードが有効になっています。 この変更により、それをサポートするシステムのパフォーマンスが向上します。
  * 64 KB のメモリページのサポート-64 KB の粒度を使用した仮想メモリの割り当ては、WDDM 2.1 でもサポートされています。 この変更は、仮想メモリページにアクセスするためのオーバーヘッドを減らすことによって、特に APUs とソケットによる恩恵を受けます。

* *現在のバッチ*処理を使用したハードウェアベースの保護されたコンテンツの改善 ([PlayReady 3.0](https://docs.microsoft.com/playready/))

* ドライバーストアによるドライバーのアップグレードの回復性を向上させるために、グラフィックスドライバーをインストールします。

* DXIL、新しいシェーダーコンパイラ言語

* D3D12 のパフォーマンスと最適化の向上

* 開発者向けの診断オプションの向上

詳細については、「 [WDDM 2.1 の機能](wddm-2-1-features.md)」を参照してください。

## <a name="wddm-20"></a>WDDM 2.0

WDDM 2.0 には、メモリ管理の更新プログラムが含まれています。

### <a name="gpu-virtual-memory"></a>GPU 仮想メモリ

* すべての物理メモリは、グラフィックス処理装置 (GPU) メモリマネージャーで管理できる仮想セグメントに抽象化されます。
* 各プロセスは、独自の GPU 仮想アドレス空間を取得します。
* スウィズリング範囲のサポートは削除されました。

詳細については、「 [WDDM 2.0 の GPU 仮想メモリ](gpu-virtual-memory-in-wddm-2-0.md)」を参照してください。

### <a name="driver-residency"></a>ドライバーの常駐

* ビデオメモリマネージャーは、ドライバーにコマンドバッファーを送信する前に、割り当てがメモリ内に存在することを確認します。 この機能を容易にするために、新しいユーザーモードドライバーデバイスドライバーのインターフェイス (DDIs) が追加されました ([*Makeresident*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)、 [*TrimResidency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_trimresidencyset)、[*削除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb))。
* 割り当てとパッチの場所の一覧は、新しいモデルでは不要なため、段階的に廃止されます。
* ユーザーモードドライバーは、割り当ての追跡を処理するようになりました。これを可能にするために、新しい DDIs がいくつか追加されています。
* ドライバーにはメモリの量が割り当てられ、メモリの負荷に応じて調整されることが予想されます。 これにより、ユニバーサル Windows ドライバーをアプリケーションプラットフォーム間で機能させることができます。
* プロセスの同期とコンテキストの監視のために、新しい DDIs が追加されました。

詳細については、 [WDDM 2.0 の「ドライバーの](driver-residency-in-wddm-2-0.md)使用」を参照してください。
