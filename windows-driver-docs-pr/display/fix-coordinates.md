---
title: FIX 座標
description: FIX 座標
ms.assetid: dfa5c61f-9464-4c63-998e-7fee21cfd278
keywords:
- ネゴシエーション WDK GDI や修正プログラムの座標を画面します。
- 小数の座標 WDK GDI
- 修正プログラムは、WDK GDI を調整します。
- ベジエ曲線 WDK GDI
- WDK GDI の行
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 588dbdfa8a62c2de5994cefe29049184872e038b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327913"
---
# <a name="fix-coordinates"></a>FIX 座標


## <span id="ddk_fix_coordinates_gg"></span><span id="DDK_FIX_COORDINATES_GG"></span>


グラフィックス Ddi は、デバイス画面のピクセルの 1/16 の場所を指定することができますを小数部の座標を使用します。 (ベクトル デバイスは、小数の座標はデバイスの解像度よりも 16 倍精度) です。小数の座標は、符号付き 28.4 ビット修正プログラムの表記法で 32 ビットの数値として表されます。 この表記法で最上位の 28 ビットは、座標の整数部を表すし、最下位 4 ビットは、小数部を表します。 たとえば、0x0000003C equals +3.7500、および 0xFFFFFFE8-1.5000 に相当します。

線、ベジエ曲線の座標は制御点を修正します。 特定のオブジェクトは、四角形クリップのリージョンなど GDI を使用して 32 ビット符号付き整数の座標を表します。 整数の座標の最大 5 ビットがクリア all または all のいずれかの座標は 28 ビット数であるため、設定します。

 

 





