---
title: W バッファリング DDI
description: W バッファリング DDI
ms.assetid: eb1270c3-0eaa-47a4-8fc6-53aea981b597
keywords:
- Direct3D WDK Windows 2000 の表示、w バッファリング
- WDK Direct3D の w バッファリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7582dfdfcf86ac7b90ee630c743efb6e8f72d67b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380519"
---
# <a name="w-buffering-ddi"></a>W バッファリング DDI


## <span id="ddk_w_buffering_ddi_gg"></span><span id="DDK_W_BUFFERING_DDI_GG"></span>


ドライバーで w バッファリングをサポート、D3DPRASTERCAPS を有効にして\_で WBUFFER キャップ、 **dwRasterCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体。 D3DRENDERSTATE\_w バッファリングまたは z バッファーを有効または無効にするドライバーに渡されるが ZENABLE レンダリング状態。

[ **D3DHAL\_DP2VIEWPORTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2viewportinfo)構造体は、平面をワールド空間の前面と背面のクリップに対応するフィールドをサポートしています (hither と変えようそれぞれ)。 この情報は、調整霧テーブルも使用できます。

 

 





