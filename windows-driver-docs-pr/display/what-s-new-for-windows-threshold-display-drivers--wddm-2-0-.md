---
title: Windows 10 のディスプレイ ドライバーの新機能については (WDDM 2.x)
description: ディスプレイ ドライバーの Windows 10 の新機能について説明します
ms.assetid: 619175D4-98DA-4B17-8F6F-71B13A31374D
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: b4482bf4ba125771a38f8d66efe9c81ec394718d
ms.sourcegitcommit: 68bfa1f69229b7ac29d0e98f049734f5bc566a30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58187467"
---
# <a name="whats-new-for-windows-10-display-drivers-wddm-20-and-later"></a>Windows 10 のディスプレイ ドライバー (WDDM 2.0 以降) の新機能については

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