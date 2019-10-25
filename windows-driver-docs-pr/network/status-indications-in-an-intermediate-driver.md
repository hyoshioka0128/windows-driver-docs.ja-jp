---
title: 中間ドライバーでの状態表示
description: 中間ドライバーでの状態表示
ms.assetid: be8d50f9-4a8d-4f3c-a507-e64dedff9a3e
keywords:
- 中間ドライバー WDK ネットワーク、状態のインジケーター
- NDIS 中間ドライバー WDK、状態のインジケーター
- WDK ネットワーク、中間ドライバーの状態を示す状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b5b9cab345edba69f1236bf883715140e45ea4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841824"
---
# <a name="status-indications-in-an-intermediate-driver"></a>中間ドライバーでの状態表示





中間ドライバーでのステータスインジケーターの実装は、プロトコルドライバーでの実装とほぼ同じです。 中間ドライバーの状態の表示の詳細については、「[プロトコルドライバーのステータスの](status-indications-in-a-protocol-driver.md)表示」を参照してください。

中間ドライバーは、状態を示すメッセージを受信すると、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出して上位レベルのドライバーまでの状態を示すことができます。 中間ドライバーは、特定の設計要件に応じて、関連するドライバーの状態の変化を示す必要があります。

 

 





