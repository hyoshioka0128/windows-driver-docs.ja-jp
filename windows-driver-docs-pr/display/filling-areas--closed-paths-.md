---
title: 塗りつぶし領域 (閉じたパス)
description: 塗りつぶし領域 (閉じたパス)
ms.assetid: 9dda1f0f-90e7-480b-aaeb-cb7781a1fe6c
keywords:
- GDI WDK Windows 2000 の表示、パスを閉じる
- グラフィック ドライバー WDK Windows 2000 の表示、閉じられたパス
- 閉じられた WDK GDI や、パスの描画
- 閉じられた WDK GDI のパスを入力します。
- 閉じられた WDK の GDI のパス
- 閉じたパス WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeda151274b9a402f70d2263f5d106ead8c52805
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573473"
---
# <a name="filling-areas-closed-paths"></a>塗りつぶし領域 (閉じたパス)


## <span id="ddk_filling_areas__28_closed_paths_29_gg"></span><span id="DDK_FILLING_AREAS__28_CLOSED_PATHS_29_GG"></span>


線の描画のようにピクセルがいっぱいになるは、整数の座標であると見なされます。 左側で、パスのセグメントを右、リージョンでは、各スキャン ラインが囲まれます。 左と右の境界線間のピクセルが塗りつぶし領域の内側と見なされます。 左側の境界に正確にピクセルが内部でもが、右側の境界線に正確には除外されます。 上罫線が正確に水平方向の場合は、任意のピクセルの境界に正確には内で下の境界線に正確にピクセルが除外されます。

次の図は、領域の左および右の境界線を基準とした塗りつぶし領域内に含まれるピクセルを決定する方法を示します。 数学的に説明すると、領域は、左と上、"closed"して、右側と下部には、"open"と見なされます。

![塗りつぶし領域内に含まれるピクセルの決定を示す図](images/fillbdy.png)

上記で説明した塗りつぶし領域の x 軸の規則は、左の境界線上罫線と下境界線の右境界線を置き換えることにより、y 軸にも当てはまります。

 

 





