---
title: エクステントの調整
description: エクステントの調整
ms.assetid: b3562744-375a-4d6f-be09-e28314282faa
keywords:
- Direct3D WDK Windows 2000 の表示、エクステントの調整
- エクステント調整 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aa4b75f3c6d50e75a3383e4793c9a8749d59882
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527433"
---
# <a name="extents-adjustment"></a>エクステントの調整


## <span id="ddk_extents_adjustment_gg"></span><span id="DDK_EXTENTS_ADJUSTMENT_GG"></span>


一部のハードウェアでは、画面スペースの頂点によって定義されているエクステントの四角形の外側のピクセルに影響を与えるアンチエイリアシング カーネルを使用します。 D3DCLIPSTATUS 構造体の範囲の四角形を使用するアプリケーション (で定義されている*d3dtypes.h*) ダーティな四角形の処理範囲の四角形では、ピクセルについては説明しませんので、レンダリング アーティファクトが発生可能性がありますハードウェアによって変更します。

Direct3D では、この問題を解決によって指定された数のピクセルの四角形が外向き調整されることを要求するハードウェアのドライバーを有効にすると、 **dvExtentsAdjust**のメンバー、 [ **D3DHAL\_D3DEXTENDEDCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff544753)構造体。 このメンバーは、GUID への応答で入力\_で D3DExtendedCaps GUID [ **DdGetDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff549404)します。 範囲の四角形は、デバイスのレンダー ターゲットのサーフェイスのエクステントにクリッピングされます。 既定値は 0 です。

 

 





