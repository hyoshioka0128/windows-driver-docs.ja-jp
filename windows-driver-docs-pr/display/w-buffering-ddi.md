---
title: W バッファリング DDI
description: W バッファリング DDI
ms.assetid: eb1270c3-0eaa-47a4-8fc6-53aea981b597
keywords:
- Direct3D WDK Windows 2000 の表示、w バッファリング
- WDK Direct3D の w バッファリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 162a51e816114945fb1824fcd6713e90fa0fba3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553053"
---
# <a name="w-buffering-ddi"></a>W バッファリング DDI


## <span id="ddk_w_buffering_ddi_gg"></span><span id="DDK_W_BUFFERING_DDI_GG"></span>


ドライバーで w バッファリングをサポート、D3DPRASTERCAPS を有効にして\_で WBUFFER キャップ、 **dwRasterCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)構造体。 D3DRENDERSTATE\_w バッファリングまたは z バッファーを有効または無効にするドライバーに渡されるが ZENABLE レンダリング状態。

[ **D3DHAL\_DP2VIEWPORTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff545936)構造体は、平面をワールド空間の前面と背面のクリップに対応するフィールドをサポートしています (hither と変えようそれぞれ)。 この情報は、調整霧テーブルも使用できます。

 

 





