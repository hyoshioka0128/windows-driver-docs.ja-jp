---
title: DC 始点
description: DC 始点
ms.assetid: 7e997f6b-fec4-4aa4-b0ed-0d02cb3f844d
keywords:
- 配信元の DC WDK GDI
- ネゴシエーション WDK GDI、DC の配信元を画面します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c81d8a2f2c936af10d8bb7c5725525a1b707a204
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578272"
---
# <a name="dc-origin"></a>DC 始点


## <span id="ddk_dc_origin_gg"></span><span id="DDK_DC_ORIGIN_GG"></span>


2²⁷ ピクセル 2²⁷ の配列内のグラフィックスを保持するアプリケーション プログラムが必要です。 デバイスの領域がある DDI レベルのウィンドウ マネージャーは、アプリケーションの座標系の符号付きの 1 つの 27 ビット座標をオフセット可能性がありますので、グラフィックスの他のサイズ、 *DC 原点*します。 DC の配信元が、ドライバーに表示されないとオフセットが適用された後にのみ、ドライバーはグラフィックスの座標を識別します。

 

 





