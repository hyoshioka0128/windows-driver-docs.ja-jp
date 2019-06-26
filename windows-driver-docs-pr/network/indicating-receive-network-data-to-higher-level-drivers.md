---
title: 高レベル ドライバーへの受信ネットワーク データの表示
description: 高レベル ドライバーへの受信ネットワーク データの表示
ms.assetid: 27272427-86bc-4fd3-bd2f-12d94273fcd4
keywords:
- 中間ドライバー WDK ネットワー キング、受信操作
- NDIS は、ドライバー WDK を中間、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3c8b81ecd6cd88967ac5e27101ddf148aa53c7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380918"
---
# <a name="indicating-receive-network-data-to-higher-level-drivers"></a>高レベル ドライバーへの受信ネットワーク データの表示





コネクションレス中間ドライバーでは、呼び出すことで、[次へ] 以上のドライバーをネットワーク データを受信を示す、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数。 接続指向の中間ドライバーでは、呼び出すことで、[次へ] 以上のドライバーをネットワーク データを受信を示す、 [ **NdisMCoIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)関数。

前に、受信ネットワーク データより高度なドライバーで、データは、おそらく、形式に変換することが想定されているドライバーのプロセスを示すと、必要な場合は、中間にドライバーで割り当てられたに関連付けられているMDLsに関連するデータをコピー[**NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。

 

 





