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
ms.openlocfilehash: 40b9245151e32fa40d4ec69aa99b8b5d26c63889
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358500"
---
# <a name="opening-and-closing-a-parallel-port"></a>パラレル ポートの開始と終了





クライアントは、パラレル ポートを共有できます。 クライアントは、クライアントが他の I/O 要求を使用して、または使用前にパラレル ポート上のファイルを開く必要があります、[ポート コールバック ルーチンを並列](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 クライアントは、クライアントがポートでは、そのファイルを閉じた後、パラレル ポートと通信する必要があります試行しません。

プラグ アンド プレイ環境でデバイスを削除したり、上、開いているファイルがないときに追加されるに注意してください。 一般に、パラレル ポートが追加されるたびにプラグ アンド プレイが別の場所とリソースを割り当てます。

 

 




