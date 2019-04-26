---
title: パレット化テクスチャ
description: パレット化テクスチャ
ms.assetid: 031739fe-32ee-46f1-a32a-de84f17eb528
keywords:
- DirectX 8.0 リリースのノート WDK Windows 2000 を表示するテクスチャのパレット
- WDK DirectX 8.0 のテクスチャ
- パレットのテクスチャ WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05ba64d33f781c76d6424e580e866251f85a18e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352400"
---
# <a name="palletized-textures"></a>パレット化テクスチャ


## <span id="ddk_palettized_textures_gg"></span><span id="DDK_PALETTIZED_TEXTURES_GG"></span>


DirectX 8.0 のパレットのテクスチャの API のサポートが変更された、ですが、DDI でこれは反映されません。 既存のパレット指向 DP2 トークンのパレットに更新プログラムのパレットおよびテクスチャの間のバインドのドライバーに通知するために使用され続けます。

これは、ことはできませんと見なされます、D3DDP2OP とサーフェスとパレット間の関連付けが確立されているため\_SETPALETTE を**lpPalette**有効なパレットを構造体の表面のポイントのフィールド。 パレットと DP2 ストリームによって確立されている画面間の関連付けは、実際の画面とパレットのデータ構造には反映されません。

さらに、DirectDraw のパレット DDI エントリ ポイントは、これらのパレットには呼び出されません。 テクスチャのパレットの操作のすべての DDI 通知は DP2 ストリームを介して行われます。

 

 





