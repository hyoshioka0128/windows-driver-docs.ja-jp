---
title: DirectX 8.0 ドライバーの最小機能要件
description: DirectX 8.0 ドライバーの最小機能要件
ms.assetid: 8c939013-516c-4048-8de5-e95529891ac9
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 の表示、レポート機能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e70d3cfc92482174036b29d8b1eacb726738eb87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840567"
---
# <a name="minimum-capability-requirements-for-directx-80-drivers"></a>DirectX 8.0 ドライバーの最小機能要件


## <span id="ddk_minimum_capability_requirements_for_directx_8_0_drivers_gg"></span><span id="DDK_MINIMUM_CAPABILITY_REQUIREMENTS_FOR_DIRECTX_8_0_DRIVERS_GG"></span>


DirectX 8.0 ランタイムには、 **GetDriverInfo2**クエリに応答して D3DCAPS8 データ構造を返すだけでなく、ドライバーが directx 8.0 レベルのドライバーと見なされるために満たす必要があるその他の要件があります。

DirectX 8.0 ドライバーは、明示的に次のことを行う必要があります。

-   D3DCAPS8 の**Maxstreams**フィールドに1つ以上の頂点ストリームがサポートされていることをレポートします。

-   D3DCAPS8 の**MaxPointSize**フィールドで、少なくとも1つのポイントスプライトの最大サイズを報告します。

-   新しいスタイルピクセル形式の仕様をサポートするように、サポートされているテクスチャ形式の一覧を変更します。

-   新しい[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) (DP2) の描画トークンを処理します。

-   ドライバーがビデオメモリの頂点バッファーの作成をサポートしていない場合でも、頂点バッファーとインデックスバッファーの[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)を処理します。 システムメモリの頂点とインデックスバッファーのハンドルは、ドライバーに渡されます。

-   ハードウェアがポスト変換された頂点データのクリッピングをサポートする場合は、新しいポスト変換されたクリッピングフラグ D3DPMISCCAPS\_CLIPTLVERT を設定します。

ピクセルまたは頂点シェーダー、ボリュームテクスチャ、ポイントスプライト (ゼロ以外の最大ポイントサイズを超える)、マルチサンプリング、または複数の頂点ストリーム (ドライバーが可能であるため) を8.0 サポートするためにドライバーが必要ではないことに注意してください。DirectX 8.0 ドライバーと見なされるようにするために、同時頂点ストリームの最大数を1に設定します)。

 

 





