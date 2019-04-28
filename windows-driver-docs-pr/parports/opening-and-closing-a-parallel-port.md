---
title: パラレル ポートの開始と終了
description: パラレル ポートの開始と終了
ms.assetid: 2183ffd9-8265-4848-b5d1-703643e0d0e6
keywords:
- パラレル ポートを開く WDK
- パラレル ポートを閉じる WDK
- パラレル ポート、WDK の共有
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94e66a666784484a185eb8253754d335578a2363
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373484"
---
# <a name="opening-and-closing-a-parallel-port"></a>パラレル ポートの開始と終了





クライアントは、パラレル ポートを共有できます。 クライアントは、クライアントが他の I/O 要求を使用して、または使用前にパラレル ポート上のファイルを開く必要があります、[ポート コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544307)します。 クライアントは、クライアントがポートでは、そのファイルを閉じた後、パラレル ポートと通信する必要があります試行しません。

プラグ アンド プレイ環境でデバイスを削除したり、上、開いているファイルがないときに追加されるに注意してください。 一般に、パラレル ポートが追加されるたびにプラグ アンド プレイが別の場所とリソースを割り当てます。

 

 




