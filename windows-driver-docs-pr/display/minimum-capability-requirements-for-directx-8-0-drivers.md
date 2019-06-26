---
title: DirectX 8.0 ドライバーの最低限の機能要件
description: DirectX 8.0 ドライバーの最低限の機能要件
ms.assetid: 8c939013-516c-4048-8de5-e95529891ac9
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示するレポートの機能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe8603dc06fde4babcd6f6e40f0c0ce46c9fc82f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385597"
---
# <a name="minimum-capability-requirements-for-directx-80-drivers"></a>DirectX 8.0 ドライバーの最低限の機能要件


## <span id="ddk_minimum_capability_requirements_for_directx_8_0_drivers_gg"></span><span id="DDK_MINIMUM_CAPABILITY_REQUIREMENTS_FOR_DIRECTX_8_0_DRIVERS_GG"></span>


応答で D3DCAPS8 データ構造体を返すことに加えて、 **GetDriverInfo2**クエリ、DirectX 8.0 ランタイムが DirectX 8.0 レベルのドライバーと見なされるドライバーが満たす必要のあるその他の要件。

DirectX 8.0 ドライバーには明示的にする必要があります。

-   レポートの 1 つまたは複数の頂点のストリームのサポート、 **MaxStreams** D3DCAPS8 のフィールド。

-   レポートで少なくとも 1 つの最大ポイント スプライトのサイズ、 **MaxPointSize** D3DCAPS8 のフィールド。

-   新しいスタイルのピクセル形式の仕様をサポートするためにサポートされているテクスチャ形式の一覧を変更します。

-   新しい処理[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) (DP2) 描画トークンです。

-   処理[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)の頂点とインデックス バッファーには、ドライバーはビデオ メモリ頂点バッファーの作成をサポートしていない場合でもです。 システム メモリの頂点とインデックス バッファーのハンドルは、ドライバーに渡されます。

-   新しい posttransformed クリッピング フラグ D3DPMISCCAPS\_CLIPTLVERT、ハードウェアのクリッピングをサポートしている場合は、頂点データを posttransformed します。

ピクセルまたは頂点シェーダー、テクスチャのボリュームなどの DirectX 8.0 の新機能のいずれかをサポートするために、ドライバーが必要ないことに注意してください (ように、ドライバーは、(0 以外の値の最大ポイント サイズ) を超えるスプライト、マルチ サンプリングまたは複数の頂点のストリームをポイント頂点の同時ストリームの最大数は、いずれかに設定)、DirectX 8.0 ドライバーと見なされるようにします。

 

 





