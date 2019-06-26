---
title: 中間ドライバーでの状態表示
description: 中間ドライバーでの状態表示
ms.assetid: be8d50f9-4a8d-4f3c-a507-e64dedff9a3e
keywords:
- 中間ドライバー WDK ネットワー キング、状態インジケーター
- NDIS 中間ドライバー WDK、状態インジケーター
- 状態インジケーター WDK、中間ネットワーク ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58ecc228e539d4b6fc41891ff6befe65dc401963
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383607"
---
# <a name="status-indications-in-an-intermediate-driver"></a>中間ドライバーでの状態表示





中間ドライバーで状態インジケーターの実装では、プロトコル ドライバーに実装するとほぼ同じです。 ドライバーの中間状態のインジケーターの詳細については、次を参照してください。[プロトコル ドライバーに状態インジケーター](status-indications-in-a-protocol-driver.md)します。

呼び出すことによってより高度なドライバーまで、状態を示す値を示している可能性、中間ドライバーでは、状態を示す値を受信すると[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)します。 中間のドライバーには、その特定のデザイン要件に合わせて上にあるドライバーへの状態の変更が示されます。

 

 





