---
title: エクステントの調整
description: エクステントの調整
ms.assetid: b3562744-375a-4d6f-be09-e28314282faa
keywords:
- Direct3D WDK Windows 2000 display、extents 調整
- エクステント調整 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c06790f1507db5df060949eca10496422b0d7dec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839695"
---
# <a name="extents-adjustment"></a>エクステントの調整


## <span id="ddk_extents_adjustment_gg"></span><span id="DDK_EXTENTS_ADJUSTMENT_GG"></span>


一部のハードウェアでは、画面領域の頂点によって定義されるエクステント四角形の外側のピクセルに影響を与えるアンチエイリアシングカーネルを使用しています。 D3DCLIPSTATUS 構造体 (d3dtypes で定義されて*います*) のエクステント四角形を使用してダーティ四角形処理を行うアプリケーションでは、エクステント四角形はハードウェアによって変更されたピクセルをカバーしないため、レンダリングアイテムが発生する可能性があります。

Direct3D は、この問題に対処するために、ハードウェアドライバーが、 [**D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)構造体の**dvExtentsAdjust**メンバーの指定されたピクセル数だけ外側にエクステント四角形を調整するように要求します。 このメンバーは、 [**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)の Guid\_D3DExtendedCaps guid に応答して入力されます。 エクステント四角形は、デバイスのレンダーターゲットサーフェイスの範囲にクリップされます。 既定値は 0 です。

 

 





