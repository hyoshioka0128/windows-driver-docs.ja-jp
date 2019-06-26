---
title: NDIS ポートの識別
description: NDIS ポートの識別
ms.assetid: 40917e62-5424-4c46-9b5b-a1a15812ef59
keywords:
- WDK NDIS、identifyng のポート
- NDIS ポート WDK、identifyng
- identifyng NDIS ポート
- ポート番号の WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e300f9b14e3bbe3eae24ec3c47ef3b86f2f7ca38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384551"
---
# <a name="identifying-an-ndis-port"></a>NDIS ポートの識別





NDIS、ポートは、そのポート番号によって識別されます。 ミニポート ドライバーを呼び出すと、 [ **NdisMAllocatePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocateport)関数、ポートの割り当てを割り当ての NDIS およびポートに最下位の使用可能なポート番号を割り当てます。 ミニポート ドライバーを呼び出すと、 [ **NdisMFreePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)ポートを解放する機能、NDIS も NDIS は、ポート番号を再利用できるように、解放されたポートに割り当てられているポート番号を解放します。

ポートごとに別のコンテキストの領域は、ドライバーは、ドライバーは、対応するコンテキストの領域にポート番号を変換するため効率的なアルゴリズムを提供する必要があります。

 

 





