---
title: レポートの最上位のサーフェスのサポート
description: レポートの最上位のサーフェスのサポート
ms.assetid: cf214ed7-2c06-4dc6-8c73-c2a3f51332ab
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示する上位サーフェスは、レポートのサポート
- 上位サーフェスの WDK DirectX 8.0、レポートのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 633b7d35177d76c9092c8eef1e4bc0f0aff0c120
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560740"
---
# <a name="reporting-support-for-high-order-surfaces"></a>レポートの最上位のサーフェスのサポート


## <span id="ddk_reporting_support_for_high_order_surfaces_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_HIGH_ORDER_SURFACES_GG"></span>


ドライバーがレポート内の 4 つの新しい機能 bits を使用して上位サーフェスのサポート、 **DevCaps** D3DCAPS8 構造体のフィールド。 これらのフラグは次のとおりです。

### <a name="span-idd3ddevcapsquinticrtpatchesspanspan-idd3ddevcapsquinticrtpatchesspand3ddevcapsquinticrtpatches"></a><span id="d3ddevcaps_quinticrtpatches"></span><span id="D3DDEVCAPS_QUINTICRTPATCHES"></span>D3DDEVCAPS\_QUINTICRTPATCHES

デバイスは、5 次ベジエ スプラインおよび B スプラインをサポートします。

### <a name="span-idd3ddevcapsrtpatchesspanspan-idd3ddevcapsrtpatchesspand3ddevcapsrtpatches"></a><span id="d3ddevcaps_rtpatches"></span><span id="D3DDEVCAPS_RTPATCHES"></span>D3DDEVCAPS\_RTPATCHES

デバイスは、四角形と三角形の修正プログラムをサポートします。

### <a name="span-idd3ddevcapsrtpatchhandlezerospanspan-idd3ddevcapsrtpatchhandlezerospand3ddevcapsrtpatchhandlezero"></a><span id="d3ddevcaps_rtpatchhandlezero"></span><span id="D3DDEVCAPS_RTPATCHHANDLEZERO"></span>D3DDEVCAPS\_RTPATCHHANDLEZERO

このデバイスの機能がセット、ハードウェア アーキテクチャにすべての情報のキャッシュが不要し、キャッシュされていないの修正プログラム (処理) がキャッシュされているものとして効率的に描画される場合。 注その D3DDEVCAPS\_RPATCHHANDLERZERO に 0 のハンドルを持つ修正プログラムが描画されることがありません。 ハンドルが 0 の修正プログラムは、この上限を設定すると、かどうかに常に描画できます。

### <a name="span-idd3ddevcapsnpatchesspanspan-idd3ddevcapsnpatchesspand3ddevcapsnpatches"></a><span id="d3ddevcaps_npatches"></span><span id="D3DDEVCAPS_NPATCHES"></span>D3DDEVCAPS\_NPATCHES

デバイスは、n 更新プログラムをサポートします。

 

 





