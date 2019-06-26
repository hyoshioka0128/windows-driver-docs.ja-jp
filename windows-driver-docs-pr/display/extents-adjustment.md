---
title: エクステントの調整
description: エクステントの調整
ms.assetid: b3562744-375a-4d6f-be09-e28314282faa
keywords:
- Direct3D WDK Windows 2000 の表示、エクステントの調整
- エクステント調整 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e34dbdf74c36c25f58883e7b92bc454f1329202
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381850"
---
# <a name="extents-adjustment"></a>エクステントの調整


## <span id="ddk_extents_adjustment_gg"></span><span id="DDK_EXTENTS_ADJUSTMENT_GG"></span>


一部のハードウェアでは、画面スペースの頂点によって定義されているエクステントの四角形の外側のピクセルに影響を与えるアンチエイリアシング カーネルを使用します。 D3DCLIPSTATUS 構造体の範囲の四角形を使用するアプリケーション (で定義されている*d3dtypes.h*) ダーティな四角形の処理範囲の四角形では、ピクセルについては説明しませんので、レンダリング アーティファクトが発生可能性がありますハードウェアによって変更します。

Direct3D では、この問題を解決によって指定された数のピクセルの四角形が外向き調整されることを要求するハードウェアのドライバーを有効にすると、 **dvExtentsAdjust**のメンバー、 [ **D3DHAL\_D3DEXTENDEDCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)構造体。 このメンバーは、GUID への応答で入力\_で D3DExtendedCaps GUID [ **DdGetDriverInfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)します。 範囲の四角形は、デバイスのレンダー ターゲットのサーフェイスのエクステントにクリッピングされます。 既定値は 0 です。

 

 





