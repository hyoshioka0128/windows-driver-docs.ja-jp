---
title: 変換済みの頂点のクリッピング
description: 変換済みの頂点のクリッピング
ms.assetid: 33b03264-780e-4b05-a108-6d1a017e8c27
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートの表示、変換済みの頂点をクリッピング
- pretransformed 頂点 WDK DirectX 8.0
- クリッピング WDK DirectX 8.0
- WDK DirectX 8.0 をクリッピング頂点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1ced8e7305e8c15daa07fd1032ed51eaef4043c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580000"
---
# <a name="clipping-transformed-vertices"></a>変換済みの頂点のクリッピング


## <span id="ddk_clipping_transformed_vertices_gg"></span><span id="DDK_CLIPPING_TRANSFORMED_VERTICES_GG"></span>


Direct3D 8.0 ランタイムの両方を通じて pretransformed 頂点のクリッピングを完全にサポートする、 **DrawPrimitive**と**ProcessVertices** API 呼び出し。 この領域には、ユーザー定義のクリップの面だけ Z および X と Y のビューポートの範囲が含まれています。 ただし、ランタイムでは、posttransformed 頂点のクリッピングは保証されません。 Posttransformed 頂点データは、ランタイムによって、ドライバーをアプリケーションから直接渡されます。 ドライバーが posttransformed 頂点データを完全にクリップする必要があるわけです。 新しい機能フラグ D3DPMISCCAPS\_DirectX 8.0 CLIPTLVERTS が追加されました。 ドライバーこのフラグを設定する場合、 **PrimitiveMiscCaps** D3DCAPS8 構造、アプリケーションのフィールドは、ドライバーは、Z をビューポートの X と Y の範囲の posttransformed 頂点データを完全にクリップを想定できます。 Posttransformed データの領域をユーザー定義のクリップ面がサポートされていることはありません。 アプリケーションが (少なくとも) x guard バンド エクステント posttransformed データにされ、Z のエクステントのクリッピングを実行するために必要な場合は、ドライバーは、このフラグを設定していない、Y とします。

ランタイムは検証されません、アプリケーションが posttransformed データを正しくクリップされるに注意してください。 重要です。 クラッシュやハングが発生しないことこのフラグが設定されている場合、クリッピングを行わない、または誤ってクリップされたデータが渡されたかどうかのドライバーの責任になります。

 

 





