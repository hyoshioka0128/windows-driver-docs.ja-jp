---
title: 32 ビット インデックスに対するサポートのレポート
description: 32 ビット インデックスに対するサポートのレポート
ms.assetid: e9ea5f0e-9b95-4671-a947-55692eca8902
keywords:
- DirectX 8.0 リリース ノートには、Windows 2000 の WDK 表示インデックス バッファー
- インデックス バッファー WDK Directx 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8db61dd470f7d506a94ed0242544809ae0f89bcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383252"
---
# <a name="reporting-support-for-32-bit-indices"></a>32 ビット インデックスに対するサポートのレポート


## <span id="ddk_reporting_support_for_32_bit_indices_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_32_BIT_INDICES_GG"></span>


DirectX 8.0 では、前に、頂点のインデックスは、16 ビットの数に制限されていました。 DirectX 8.0 では、32 ビットのインデックスのサポートを追加します。 ドライバーでは、32 ビットのインデックスのサポートをレポートの値を設定して、 **MaxVertexIndex** D3DCAPS8 のフィールド (現在もで[ **D3DHAL\_D3DEXTENDEDCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff544753)) 0 xffff より大きい値にします。 このフィールドは、レポートを 32 ビットの記憶域を必要とするインデックスをサポートして ことはできませんの 32 ビット値の完全な範囲にドライバーもできます。

**DirectX 9.0 と以降のバージョンのみ。**

 

ドライバー、ドライバー、Direct3D ハードウェア アブストラクション レイヤー (HAL) デバイス DirectX 9.0 インターフェイス経由でアプリケーションを公開するためには、値を設定する必要があります**MaxVertexIndex** 0 xffff 以上の値にします。
 

 





