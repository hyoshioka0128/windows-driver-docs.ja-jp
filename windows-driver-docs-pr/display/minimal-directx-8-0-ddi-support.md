---
title: DirectX 8.0 DDI の最小サポート
description: DirectX 8.0 DDI の最小サポート
ms.assetid: 8758e25e-e54f-42e5-a23d-354af634bce9
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、最小限のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a2d4856352050b859e3b6de12fbd71774fbf6bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840568"
---
# <a name="minimal-directx-80-ddi-support"></a>DirectX 8.0 DDI の最小サポート


## <span id="ddk_minimal_directx_8_0_ddi_support_gg"></span><span id="DDK_MINIMAL_DIRECTX_8_0_DDI_SUPPORT_GG"></span>


Directx 8.0 では、DirectX 7.0 レベルのドライバーによってハードウェアアクセラレータが提供されます。 ただし、ドライバーで、複数の頂点ストリーム、インデックスバッファー、または頂点とピクセルシェーダーなどの DirectX 8.0 の新機能を公開するには、DirectX 8.0 のスタイル機能を報告し、新しい[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)をサポートする必要があります。レンダリングトークン。 新しい D3dDrawPrimitives2 レンダリングトークンをサポートするために、ドライバーは頂点ストリームと固定関数の頂点シェーダーの基本的なサポートを提供する必要があります。

DirectX 8.0 スタイル機能の報告には、次の手順が含まれます。

-   既存の[**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)エントリポイントの新しい**GetDriverInfo2** variant を処理します。

-   要求されたときに、デバイスの機能を含む D3DCAPS8 構造体を返します。

-   構造体の定義済みフィールドに特定の最小値があることを確認します。

-   DirectX 8.0 スタイルの形式の説明を含むテクスチャ形式の一覧を返します。

以下のセクションでは、これらのさまざまな要件について説明します。

 

 





