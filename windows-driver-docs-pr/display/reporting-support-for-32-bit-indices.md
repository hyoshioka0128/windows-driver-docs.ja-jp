---
title: 32 ビット インデックスに対するサポートのレポート
description: 32 ビット インデックスに対するサポートのレポート
ms.assetid: e9ea5f0e-9b95-4671-a947-55692eca8902
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、インデックスバッファー
- インデックスバッファー (WDK Directx 8.0)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8708676d8110702118d4275eb59ece7a38440bce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829592"
---
# <a name="reporting-support-for-32-bit-indices"></a>32 ビット インデックスに対するサポートのレポート


## <span id="ddk_reporting_support_for_32_bit_indices_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_32_BIT_INDICES_GG"></span>


DirectX 8.0 より前では、頂点インデックスは16ビットの数量に制限されていました。 DirectX 8.0 では、32ビットのインデックスのサポートが追加されます。 ドライバーは、D3DCAPS8 の**Maxvertexindex**フィールド (現在も[**D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)) の値を0xffff よりも大きい値に設定することにより、32ビットのインデックスをサポートしていることを報告します。 また、このフィールドでは、32ビットの記憶域を必要とするインデックスをサポートしていても、32ビットの値の全範囲をサポートしていないことをドライバーから報告できます。

**DirectX 9.0 以降のバージョンのみ。**

 

ドライバーが DirectX 9.0 インターフェイスを介して Direct3D hardware アブストラクションレイヤー (HAL) デバイスをアプリケーションに公開するためには、ドライバーは**Maxvertexindex**の値を0xffff 以上の値に設定する必要があります。
 

 





