---
title: W バッファリング DDI
description: W バッファリング DDI
ms.assetid: eb1270c3-0eaa-47a4-8fc6-53aea981b597
keywords:
- Direct3D WDK Windows 2000 display、w バッファリング
- w-WDK Direct3D をバッファリングする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdc049f000df0f55cf8b891e35a646d6b2a5b1fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825234"
---
# <a name="w-buffering-ddi"></a>W バッファリング DDI


## <span id="ddk_w_buffering_ddi_gg"></span><span id="DDK_W_BUFFERING_DDI_GG"></span>


このドライバーは、 [**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**DWRASTERCAPS**メンバーで D3DPRASTERCAPS\_wbuffer cap を有効にすることで、w バッファリングをサポートしています。 D3DRENDERSTATE\_ZENABLE レンダリング状態は、w バッファリングまたは z バッファリングを有効または無効にするために、ドライバーに渡されます。

[**D3DHAL\_DP2VIEWPORTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2viewportinfo)構造体は、ワールド空間の前面クリップとバッククリップ平面に対応するフィールドをサポートしています。 この情報を使用して、霧テーブルを調整することもできます。

 

 





