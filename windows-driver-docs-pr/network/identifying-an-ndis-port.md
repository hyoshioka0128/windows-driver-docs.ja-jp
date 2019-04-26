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
ms.openlocfilehash: 71d5818dbd50554884bc245bdf8c8ec8dfeb7080
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349476"
---
# <a name="identifying-an-ndis-port"></a>NDIS ポートの識別





NDIS、ポートは、そのポート番号によって識別されます。 ミニポート ドライバーを呼び出すと、 [ **NdisMAllocatePort** ](https://msdn.microsoft.com/library/windows/hardware/ff562779)関数、ポートの割り当てを割り当ての NDIS およびポートに最下位の使用可能なポート番号を割り当てます。 ミニポート ドライバーを呼び出すと、 [ **NdisMFreePort** ](https://msdn.microsoft.com/library/windows/hardware/ff563588)ポートを解放する機能、NDIS も NDIS は、ポート番号を再利用できるように、解放されたポートに割り当てられているポート番号を解放します。

ポートごとに別のコンテキストの領域は、ドライバーは、ドライバーは、対応するコンテキストの領域にポート番号を変換するため効率的なアルゴリズムを提供する必要があります。

 

 





