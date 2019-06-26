---
title: ポインターの描画
description: ポインターの描画
ms.assetid: 5eaedf04-cbd9-4591-8cff-0087508aa7a9
keywords:
- 描画ポインター WDK Windows 2000 を表示します。
- ディスプレイ ドライバー WDK Windows 2000 では、ポインター
- Windows 2000 の WDK のポインターを表示します。
- モノクロ ポインター WDK Windows 2000 を表示します。
- Windows 2000 の WDK のポインターの色の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eb6a48f2f26749da0d7cb7fa9c3b7aad403f4d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365702"
---
# <a name="pointer-drawing"></a>ポインターの描画


## <span id="ddk_pointer_drawing_gg"></span><span id="DDK_POINTER_DRAWING_GG"></span>


GDI は、ポインターの色とモノクロ ポインターの両方をサポートします。 モノクロのポインターの形状は、1 つのビットマップによって定義されます。 ビットマップの幅は、同じように、表示がビットマップの上にポインターの幅がある垂直方向のエクステントとして 2 回、2 つのマスクを格納することができますに表示されます。

ポインターの関数に対する呼び出しは、GDI によってシリアル化されます。 つまり、ドライバーの 2 つの異なるスレッドでは、ポインター、関数を同時に実行することはできません。 2 つの可能なポインター関数があります。[**DrvSetPointerShape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)と[ **DrvMovePointer**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)します。

 

 





