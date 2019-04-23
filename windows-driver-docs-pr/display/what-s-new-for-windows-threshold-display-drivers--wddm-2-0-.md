---
title: Windows 10 のディスプレイ ドライバーの新機能については (WDDM 2.x)
description: ディスプレイ ドライバーの Windows 10 の新機能について説明します
ms.assetid: 619175D4-98DA-4B17-8F6F-71B13A31374D
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18, 19H1
ms.openlocfilehash: 0fe540b7ecd20887032f968ac2efa4f234f30f59
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903076"
---
# <a name="whats-new-for-windows-10-display-drivers-wddm-20-and-later"></a>Windows 10 のディスプレイ ドライバー (WDDM 2.0 以降) の新機能については

## <a name="wddm-26"></a>WDDM 2.6

### <a name="super-wet-ink"></a>Super ウェット インク

*超ウェット インク*中心とする機能は、*フロント バッファー レンダリング*します。 IHV ドライバーでは、形式や、ハードウェアでサポートされていないモードの「表示可能な」テクスチャの作成をサポートできます。 これは、アプリが要求したテクスチャを割り当てることによって、表示できる形式/レイアウトで「シャドウ」テクスチャとして存在する時に 2 つのコピーと共に、実行できます。 この「シャドウ」必ずしもテクスチャ考えてみるとしますが、圧縮データを単なる通常の方法でします。 さらに、その必要はありませんが存在するが、代わりに、最適化をする可能性があります。

ランタイムは、表示可能なサーフェイスのこれらの側面を理解する進化は。

* かどうか特定の VidPnSource/平面上に表示する影が存在する必要があります。

* 存在する影のより最適なかどうか。

* アプリケーションの画面からシャドウ画面に内容を転送するときにします。

    * ランタイムは、現在内で暗黙的になることではなく、この操作を明示的になります。

* 要求モードの設定や元とシャドウ サーフェスの間で動的に反転する方法。

Scanout は、VBlank、イメージの下に上から縦方向にスキャン後、間もなく開始可能性があり、[次へ] の VBlank の少し前に完了します。 これは常にピクセルのクロックのタイミングと、テクスチャ; 内のデータのレイアウトに応じて、ケース特に実際に圧縮を使用できる場合。 

分離し、理解 (可能な) 場合に、scanout する前に発生する変換は、フロント バッファーのレンダリングを有効にするは、新しい Ddi が追加されました。 参照してください[D3DWDDM2_6DDI_SCANOUT_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3dwddm2_6ddi_scanout_flags)と[PFND3DWDDM2_6DDI_PREPARE_SCANOUT_TRANSFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_6ddi_prepare_scanout_transformation)します。

### <a name="variable-rate-shading"></a>可変レートの網掛け

可変レートの網かけ、またはピクセルが粗い網掛けは、レンダリングされたイメージ間でさまざまな料金でのパフォーマンス/電源のレンダリングの割り当てを有効にするメカニズムです。

で以前のモデル、ジオメトリのエイリアスを削減する MSAA (マルチ サンプル アンチエイリアシング) を使用するには。

* ジオメトリのエイリアスを削減する量必要があります既知である初期ターゲットが割り当てられる場合。
* ターゲットが割り当てられると、ジオメトリのエイリアスを削減する量を変更できません。

新しいモデルが、反対に MSAA を拡張、WDDM 2.6 で*ピクセルが粗い*の新しい概念を追加することで、方向*粗い網掛け*します。 これは、網掛けをピクセルよりも粗い頻度で実行できます。 結果は、グループのすべてのサンプルをブロードキャストし、ピクセルのグループを 1 つの単位として網掛けことができます。

網掛けが粗い API は、影付きのグループに属しているピクセルの数を指定するアプリを使用できます。 レンダー ターゲットが割り当てられた後は、ピクセルが粗いサイズを変えることができます。 そのため、画面または別の描画パスの異なる部分では、別のコースの網掛け料金ことができます。

複数層の実装では 2 つのユーザー クエリ可能なキャップを持つです。 階層 1 と 2 は、粗い網掛けがサンプリングされた単一の両方で使用可能と MSAA リソース。 MSAA のリソースの網掛けに実行されるピクセルあたりの粗い- したり、サンプルごとのいつものようです。 ただし、層 1 と 2 は、MSAA のリソースでは、粗いサンプリングをピクセル単位とサンプルごとの間の頻度で網掛けを使用できません。

第 1 層:

* 網掛けレートはごとの描画の単位でのみ指定できます。何もするよりも細かい

* レンダー ターゲット内に設定とは無関係にどのような描画が一様に適用されますレートを網掛け  

第 2 層:

* ごとの描画-ごとに、階層 1 のように、網掛けのレートを指定できます。 およびごとの描画-ごとの組み合わせによって指定することもできます。

    * 富んだ-頂点ごと、セマンティックと
    * スクリーン空間イメージ

* 次の 3 つのソースからの網掛けの料金は、コンバイナーのセットを使用して結合されます。
* 画面領域の画像タイルのサイズは 16 x 16 以下です。 アプリから要求レートを網掛け正確に (時間およびその他の再構築のフィルターの精度) で配信することが保証されます。 

* SV_ShadingRate PS の入力がサポートされています。 あたり富んだ頂点率もここでは、プリミティブ単位のレートとして呼ばれるは、1 つのビューポートが使用され、SV_ViewportIndex に書き込まれない場合にのみ有効です。

* SupportsPerVertexShadingRateWithMultipleViewports キャップが true でマークされている場合、1 つ以上のビューポートとあたり富んだ頂点の割合、プリミティブ単位の料金とも呼ばを使用できます。 さらに、その場合は、ことができますに SV_ViewportIndex が書き込まれたとき。

参照してください[PFND3D12DDI_RS_SET_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_rs_set_shading_rate_0062)と[D3D12DDI_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/ne-d3d12umddi-d3d12ddi_shading_rate_0062)します。

### <a name="collect-diagnostic-info"></a>診断情報を収集します。

*診断情報を収集*により、OS の両方のレンダリングで構成され、関数を表示するグラフィックス アダプターのドライバーからプライベート データを収集します。 この新しい機能は、WDDM 2.6 での要件です。 

新しい DDI には、ドライバーが読み込まれる、いつでも情報を収集する OS を許可する必要があります。 現在、OS が (タイムアウト検出と回復) TDR のミニポート ドライバーのプライベート データのクエリによって実装される DxgkDdiCollectDebugInfo 関数を使用してケースに関連します。 新しい DDI は、さまざまな理由のデータの収集に使用されます。 要求されている種類の情報を提供する診断が必要なときに、OS はこの DDI を呼び出します。 ドライバーは、問題を調査し、OS に提出する重要なすべての個人情報を収集する必要があります。 DxgkDdiCollectDebugInfo は最終的に非推奨し、DxgkDdiCollectDiagnosticInfo に置き換えられます。

参照してください[DXGKDDI_COLLECTDIAGNOSTICINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_collectdiagnosticinfo)します。

### <a name="background-processing"></a>バック グラウンド処理

バック グラウンド処理は、ユーザーを表現するモード ドライバー許可し、動作、およびランタイムのスレッドを必要なコントロールまたはそのモニターにします。 ユーザー モード ドライバーはバック グラウンド スレッドをスピンアップし、可能な優先度を低くスレッドに割り当てるし、これらのスレッドがクリティカル パスのスレッド、成功した場合と通常を中断しないようにする NT スケジューラに依存します。

Api は、どのようなバック グラウンド処理量がのワークロードに対する適切なと、その作業を実行するタイミングを調整するアプリを許可します。

参照してください[PFND3D12DDI_QUEUEPROCESSINGWORK_CB_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_queueprocessingwork_cb_0062)します。

### <a name="driver-hot-update"></a>ホット アップデートのドライバー

ホット アップデートのドライバーは、OS コンポーネントを更新する必要がある場合、可能な限りサーバーのダウンタイムを減らします。

ホット パッチのドライバーを使用して、カーネル モード ドライバーにセキュリティ更新プログラムを適用します。 ここで、ドライバーはアダプターのメモリを節約するよう求められます、アダプターが停止された、ドライバーが読み込まれて、新しいドライバーが読み込まれるおよびアダプターが再び開始します。

参照してください[DXGKDDI_SAVEMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_savememoryforhotupdate)と[DXGKDDI_RESTOREMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_restorememoryforhotupdate)します。

## <a name="wddm-25"></a>WDDM 2.5

### <a name="content-changes"></a>コンテンツの変更

| トピック | 日付 | 説明 |
| --- | --- | --- |
| [EDID 拡張機能 (VSDB) HMDs し、特殊な表示](specialized-monitors-edid-extension.md) | 12/03/2018 | 表示の製造元の仕様 |
| [DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys)](directx-graphics-kernel-subsystem.md) | 12/04/2018 | Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) を通じて、Windows オペレーティング システムを実装するカーネル モード インターフェイス。 |
| [WDDM 2.1 機能](wddm-2-1-features.md) | 01/10/2019|WDDM 2.1 の新機能と更新された機能について説明します |

### <a name="raytracing"></a>Raytracing

新しい Direct3D DDI は、並列の Direct3D API の raytracing のハードウェア アクセラレーションをサポートするために作成されました。 次のような DDI があります。 

* [PFND3D12DDI_BUILD_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_build_raytracing_acceleration_structure_0054) 
* [PFND3D12DDI_COPY_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_copy_raytracing_acceleration_structure_0054)
* [PFND3D12DDI_EMIT_RAYTRACING_ACCELERATION_STRUCTURE_POSTBUILD_INFO_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_emit_raytracing_acceleration_structure_postbuild_info_0054)
* [PFND3D12DDI_GET_RAYTRACING_ACCELERATION_STRUCTURE_PREBUILD_INFO_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_get_raytracing_acceleration_structure_prebuild_info_0054)

Raytracing に関する詳細についてを参照してください。

* [Microsoft DirectX Raytracing の発表](https://blogs.msdn.microsoft.com/directx/2018/03/19/announcing-microsoft-directx-raytracing/)
* [DirectX Raytracing と Windows 10 年 2018年 10 月の更新プログラム](https://blogs.msdn.microsoft.com/directx/2018/10/02/directx-raytracing-and-the-windows-10-october-2018-update/)
* [DirectX のフォーラム](https://forums.directxtech.com/index.php?topic=5985.0)

### <a name="display-synchronization"></a>同期を表示します。

OS は、表示は、OS、表示を有効にする前にそのために、ドライバーによって公開されるときに、同期を表示するための機能確認されます。 TypeIntegratedDisplay 子デバイスでは、これが報告される呼び出しを経由して[DxgkDdiQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)で*型* [DXGKQAITYPE_INTEGRATED_DISPLAY_DESCRIPTOR2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)アダプターの初期化中に ホット プラグを使用して処理の一部として、WDDM 2.5 以降でサポートされる、TypeVideoOutput 子デバイスの機能の報告[DxgkDdiUpdateMonitorLinkInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_updatemonitorlinkinfo)に基づいているため、機能が変わる可能性があります、ターゲットまたは接続されているモニター。

OS でディスプレイの同期を指定します、 [DxgkDdiSetTimingsFromVidPn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)呼び出しの入力フィールドに、パスごと[DXGK_SET_TIMING_PATH_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_set_timing_path_info#input)構造体。

## <a name="wddm-21"></a>WDDM 2.1

WDDM 2.1 では、新しいシナリオを実現し、パフォーマンス、信頼性、アップグレードの回復性、診断の向上、Windows グラフィックス サブシステムの今後のシステムの機能強化の領域が大幅に向上を提供します。
WDDM 2.0 ドライバー モデルは D3D12 の前提条件です。 WDDM 2.0 と DirectX12 は、以降 Windows 10 でのみ利用できます。

次に機能の追加と WDDM 2.1 の更新プログラムの一覧を示します。

* グラフィックスの向上パフォーマンス オーバーヘッド時間を減らすことでは、メモリ管理と不足しているグラフィックス メモリの使用状況をより効率的に費やされました。 グラフィックスのパフォーマンスの向上は次のとおりです。

    * プランしリソースを解放 - 提供し、バック グラウンド モードで実行されているアプリケーションのメモリ使用量の短縮による改善を再利用します。
    * WDDM 2.1 では、大規模なページ テーブル エントリ (PTE) VRAM でのエンコードを 2 MB のページ テーブル エントリをエンコードするためのサポートを有効にします。 この変更では、サポートされているシステムでのパフォーマンスが向上します。
    * 64 KB のメモリ ページ - 64 KB の粒度を使用して、仮想メモリの割り当てのサポートは、WDDM 2.1 でもサポートされます。 この変更では、仮想メモリ ページにアクセスするためのオーバーヘッドを減らすことでさらなると Soc を特に利用できます。

* コンテンツの強化と保護されているハードウェア ベース*バッチ処理を提示*([PlayReady 3.0](https://docs.microsoft.com/playready/))

* ドライバーのアップグレードの回復性を向上させるためにグラフィック ドライバーをドライバー ストアのインストール。

* DXIL、新しいシェーダー コンパイラ言語

* D3D12 のパフォーマンスと最適化の機能強化

* 開発者向けの強化された診断オプション

詳細については、次を参照してください。 [WDDM 2.1 機能](wddm-2-1-features.md)します。

## <a name="wddm-20"></a>WDDM 2.0

WDDM 2.0 には、メモリ管理の更新プログラムが含まれています。

### <a name="gpu-virtual-memory"></a>GPU 仮想メモリ

-   すべての物理メモリは、グラフィックス処理ユニット (GPU) のメモリ マネージャーによって管理できる仮想セグメントに抽象化されています。
-   各プロセスは、GPU 仮想アドレス空間を取得します。
-   スウィズ リング範囲のサポートが削除されました。

詳細については、次を参照してください。 [WDDM 2.0 での GPU 仮想メモリ](gpu-virtual-memory-in-wddm-2-0.md)します。

### <a name="driver-residency"></a>ドライバーの保存場所

-   ビデオ メモリ マネージャーは、ドライバーをコマンド バッファーを送信する前に、割り当てがメモリに常駐していることを確認します。 この機能を容易に新しいユーザー モード ドライバーのデバイス ドライバー インターフェイス (Ddi) が追加されました ([*MakeResident*](https://msdn.microsoft.com/library/windows/hardware/dn906357)、 [ *TrimResidency* ](https://msdn.microsoft.com/library/windows/hardware/dn906364)、 [*削除*](https://msdn.microsoft.com/library/windows/hardware/dn906355))。
-   割り当てと修正プログラムの場所の一覧が廃止されるため、新しいモデルで必要はありません。
-   ユーザー モード ドライバーは割り当ての追跡を処理するようになりましたし、これを有効にするいくつかの新しい Ddi が追加されました。
-   ドライバーはメモリの予算を指定して、メモリ負荷の下での適応が必要です。 これは、アプリケーション プラットフォーム間で機能するユニバーサル Windows ドライバーを許可します。
-   プロセスの同期とコンテキストの監視のため、新しい Ddi が追加されました。

詳細については、次を参照してください。 [WDDM 2.0 でのドライバーの常駐](driver-residency-in-wddm-2-0.md)します。
