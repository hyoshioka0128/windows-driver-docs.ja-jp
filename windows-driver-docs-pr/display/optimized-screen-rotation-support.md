---
title: 最適化された画面回転のサポート
description: Windows 8 では、回転モードの変更時にグラフィックスアダプターからの出力が有効であることを保証することで、ちらつきなしの画面の回転を実現します。
ms.assetid: CFDB4713-EC90-4FAB-B379-742C52888BB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d3e4d1f62b1a253b83d7eb6a0e6ce08a6f0cef0
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968273"
---
# <a name="optimized-screen-rotation-support"></a>最適化された画面回転のサポート


Windows 8 では、回転モードの変更時にグラフィックスアダプターからの出力が有効であることを保証することで、ちらつきなしの画面の回転を実現します。 この機能は、回転モードをサポートするすべての Windows Display Driver Model (WDDM) 1.2 ドライバーで必要です。

**メモ**   Windows 8.1 Update 以降では、プライマリディスプレイが回転しているときに、複製されたモニターで可能な限り高い解像度をサポートするようにデバイスドライバーインターフェイス (DDIs) が更新されます。 「[パスに依存しないローテーションのサポート](supporting-path-independent-rotation.md)」を参照してください。

 

**最小 WDDM バージョン**: 1.2

**Windows の最小バージョン**: 8

**ドライバーの実装—完全なグラフィックスと表示のみ**: 必須


 

## <a name="span-idsmooth_rotation_ddispanspan-idsmooth_rotation_ddispanspan-idsmooth_rotation_ddispansmooth-rotation-ddi"></a><span id="Smooth_rotation_DDI"></span><span id="smooth_rotation_ddi"></span><span id="SMOOTH_ROTATION_DDI"></span>Smooth ローテーション DDI


これらのドライバーによって実装された関数が呼び出された場合、ディスプレイミニポートドライバーはパスローテーションの更新をサポートする必要があります。

-   [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)
-   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)

ドライバーは、Windows 8 以降で使用可能な[**DXGK \_ drivercaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)構造体の**SupportSmoothRotation**メンバーを設定することによって、 [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)の呼び出しにおける smooth ローテーションのサポートを示す必要があります。
ドライバーは、 [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)の呼び出し中に常にパスのローテーションを設定できる必要があります。

## <a name="span-idsmooth_rotation_scenariosspanspan-idsmooth_rotation_scenariosspanspan-idsmooth_rotation_scenariosspansmooth-rotation-scenarios"></a><span id="Smooth_rotation_scenarios"></span><span id="smooth_rotation_scenarios"></span><span id="SMOOTH_ROTATION_SCENARIOS"></span>Smooth ローテーションのシナリオ


従来のデスクトップおよびラップトップシステムでは、画面の回転は頻繁に使用されるシナリオではありません。 しかし、モバイルデバイスでは、多くの場合、画面の回転はメインストリームのシナリオです。 Windows 8 では、画面の回転中にモニターの同期が有効な状態を維持するために、ディスプレイインフラストラクチャに最適化を行うことができます。 次の条件に該当する場合は、エンドユーザーがスムーズに回転することができます。

-   プラットフォームは WDDM 1.2 を実行しています。
-   デスクトップコンポジションマネージャーはオンになっており、アクティブに作成されています。
-   モードの変更要求は、スムーズローテーションモードの切り替えと互換性があると判断されます。 2つのモードは、同じディメンション (幅と高さ)、トポロジ、リフレッシュレート、ピクセル形式、およびストライドがある場合に互換性があり、画面の向きだけが異なります (つまり、回転されます)。

 

 





