---
title: DirectX 8.0 ドライバーの最低限の機能要件
description: DirectX 8.0 ドライバーの最低限の機能要件
ms.assetid: 8c939013-516c-4048-8de5-e95529891ac9
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示するレポートの機能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1368535cadc96b5c9b00561c1449426c2a501189
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385026"
---
# <a name="minimum-capability-requirements-for-directx-80-drivers"></a>DirectX 8.0 ドライバーの最低限の機能要件


## <span id="ddk_minimum_capability_requirements_for_directx_8_0_drivers_gg"></span><span id="DDK_MINIMUM_CAPABILITY_REQUIREMENTS_FOR_DIRECTX_8_0_DRIVERS_GG"></span>


応答で D3DCAPS8 データ構造体を返すことに加えて、 **GetDriverInfo2**クエリ、DirectX 8.0 ランタイムが DirectX 8.0 レベルのドライバーと見なされるドライバーが満たす必要のあるその他の要件。

DirectX 8.0 ドライバーには明示的にする必要があります。

-   レポートの 1 つまたは複数の頂点のストリームのサポート、 **MaxStreams** D3DCAPS8 のフィールド。

-   レポートで少なくとも 1 つの最大ポイント スプライトのサイズ、 **MaxPointSize** D3DCAPS8 のフィールド。

-   新しいスタイルのピクセル形式の仕様をサポートするためにサポートされているテクスチャ形式の一覧を変更します。

-   新しい処理[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) (DP2) 描画トークンです。

-   処理[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)の頂点とインデックス バッファーには、ドライバーはビデオ メモリ頂点バッファーの作成をサポートしていない場合でもです。 システム メモリの頂点とインデックス バッファーのハンドルは、ドライバーに渡されます。

-   新しい posttransformed クリッピング フラグ D3DPMISCCAPS\_CLIPTLVERT、ハードウェアのクリッピングをサポートしている場合は、頂点データを posttransformed します。

ピクセルまたは頂点シェーダー、テクスチャのボリュームなどの DirectX 8.0 の新機能のいずれかをサポートするために、ドライバーが必要ないことに注意してください (ように、ドライバーは、(0 以外の値の最大ポイント サイズ) を超えるスプライト、マルチ サンプリングまたは複数の頂点のストリームをポイント頂点の同時ストリームの最大数は、いずれかに設定)、DirectX 8.0 ドライバーと見なされるようにします。

 

 





