---
title: 最小限の DirectX 8.0 DDI サポート
description: 最小限の DirectX 8.0 DDI サポート
ms.assetid: 8758e25e-e54f-42e5-a23d-354af634bce9
keywords:
- DirectX 8.0 リリース ノートには Windows 2000 の WDK の表示、最小限のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 875829941427fac96afdf08901be3c490036d1fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385599"
---
# <a name="minimal-directx-80-ddi-support"></a>最小限の DirectX 8.0 DDI サポート


## <span id="ddk_minimal_directx_8_0_ddi_support_gg"></span><span id="DDK_MINIMAL_DIRECTX_8_0_DDI_SUPPORT_GG"></span>


DirectX 8.0 では、DirectX 7.0 ドライバー、ハードウェア アクセラレーションを提供します。 ただし、複数の頂点のストリーム、インデックス バッファー、頂点とピクセル シェーダーなどの DirectX 8.0 の新機能のいずれかを公開するドライバーの場合する必要があります DirectX 8.0 スタイルの機能を報告することによって識別される、サポート、新しい[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)レンダリング トークンです。 新しい D3dDrawPrimitives2 をサポートするためには、トークン、ドライバーのレンダリング頂点ストリームと頂点シェーダーの固定機能の基本的なサポートを提供する必要があります。

DirectX 8.0 スタイルの機能をレポートには、次の手順が含まれます。

-   新しい処理**GetDriverInfo2** 、既存のバリアント[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)エントリ ポイント。

-   要求されたときに、デバイスの機能を含む D3DCAPS8 構造体を返します。

-   その構造体の定義済みのフィールドは、特定の最小値であることを確認します。

-   DirectX 8.0 スタイル サーフェスの形式の説明を含むテクスチャ形式の一覧を返します。

これらのさまざまな要件は、次のセクションについて説明します。

 

 





