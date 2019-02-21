---
title: パラレル ポートを開いたり、閉じたりします。
description: パラレル ポートを開いたり、閉じたりします。
ms.assetid: 2183ffd9-8265-4848-b5d1-703643e0d0e6
keywords:
- パラレル ポートを開く WDK
- パラレル ポートを閉じる WDK
- パラレル ポート、WDK の共有
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94e66a666784484a185eb8253754d335578a2363
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548753"
---
# <a name="opening-and-closing-a-parallel-port"></a>パラレル ポートを開いたり、閉じたりします。





クライアントは、パラレル ポートを共有できます。 クライアントは、クライアントが他の I/O 要求を使用して、または使用前にパラレル ポート上のファイルを開く必要があります、[ポート コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544307)します。 クライアントは、クライアントがポートでは、そのファイルを閉じた後、パラレル ポートと通信する必要があります試行しません。

プラグ アンド プレイ環境でデバイスを削除したり、上、開いているファイルがないときに追加されるに注意してください。 一般に、パラレル ポートが追加されるたびにプラグ アンド プレイが別の場所とリソースを割り当てます。

 

 




