---
title: 32 ビット インデックスに対するサポートのレポート
description: 32 ビット インデックスに対するサポートのレポート
ms.assetid: e9ea5f0e-9b95-4671-a947-55692eca8902
keywords:
- DirectX 8.0 リリース ノートには、Windows 2000 の WDK 表示インデックス バッファー
- インデックス バッファー WDK Directx 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 065ad0f4ab916fb6af9dec769bddccd8140d84d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369275"
---
# <a name="reporting-support-for-32-bit-indices"></a>32 ビット インデックスに対するサポートのレポート


## <span id="ddk_reporting_support_for_32_bit_indices_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_32_BIT_INDICES_GG"></span>


DirectX 8.0 では、前に、頂点のインデックスは、16 ビットの数に制限されていました。 DirectX 8.0 では、32 ビットのインデックスのサポートを追加します。 ドライバーでは、32 ビットのインデックスのサポートをレポートの値を設定して、 **MaxVertexIndex** D3DCAPS8 のフィールド (現在もで[ **D3DHAL\_D3DEXTENDEDCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)) 0 xffff より大きい値にします。 このフィールドは、レポートを 32 ビットの記憶域を必要とするインデックスをサポートして ことはできませんの 32 ビット値の完全な範囲にドライバーもできます。

**DirectX 9.0 と以降のバージョンのみ。**

 

ドライバー、ドライバー、Direct3D ハードウェア アブストラクション レイヤー (HAL) デバイス DirectX 9.0 インターフェイス経由でアプリケーションを公開するためには、値を設定する必要があります**MaxVertexIndex** 0 xffff 以上の値にします。
 

 





