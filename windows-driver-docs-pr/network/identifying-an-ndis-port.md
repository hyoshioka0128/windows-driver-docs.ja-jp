---
title: NDIS ポートの識別
description: NDIS ポートの識別
ms.assetid: 40917e62-5424-4c46-9b5b-a1a15812ef59
keywords:
- ポート WDK NDIS、識別子
- NDIS ポート WDK、識別子
- NDIS ポートの識別子
- ポート番号 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67a63ee26490bd126d2ba1174b19d13aac3573f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823826"
---
# <a name="identifying-an-ndis-port"></a>NDIS ポートの識別





NDIS ポートは、そのポート番号によって識別されます。 ミニポートドライバーがポートを割り当てるために[**NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)関数を呼び出すと、NDIS はポートに使用可能な最も小さいポート番号を割り当てて割り当てます。 ミニポートドライバーがポートを解放するために[**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)関数を呼び出すと、ndis は解放されたポートに割り当てられているポート番号も解放して、ndis がポート番号を再利用できるようにします。

ドライバーがポートごとに個別のコンテキスト領域を保持している場合、ドライバーは、対応するコンテキスト領域にポート番号を変換するための効率的なアルゴリズムを提供する必要があります。

 

 





