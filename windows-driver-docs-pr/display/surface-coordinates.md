---
title: サーフェス座標
description: サーフェス座標
ms.assetid: 1f59f135-530a-475a-92b6-f3995aa0c1bb
keywords:
- ネゴシエーション WDK GDI や画面座標を画面します。
- 画面座標を WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b8d4cd533fa558677aa58e4ff5d37623ac142dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350040"
---
# <a name="surface-coordinates"></a>サーフェス座標


## <span id="ddk_surface_coordinates_gg"></span><span id="DDK_SURFACE_COORDINATES_GG"></span>


デバイスの画面は、2²⁸ 2²⁸ ピクセルの配列のサブセットです。 これらのピクセルは 28 ビットの符号付き数値の組によってアドレス指定、デバイスの画面の左上隅のピクセルには、座標 (0, 0) が与えられます。 デバイスの画面は、両方の座標が負でない、座標空間の下の適切なセクションにあります。

 

 





