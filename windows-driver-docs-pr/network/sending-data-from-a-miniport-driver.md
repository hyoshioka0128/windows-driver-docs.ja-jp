---
title: ミニポート ドライバーからのデータの送信
description: ミニポート ドライバーからのデータの送信
ms.assetid: f82475ff-8d32-4448-9b19-b6fa97a93d32
keywords:
- データの送信 (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41e260119776a168aa13680a325a5d4d69eb3106
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841977"
---
# <a name="sending-data-from-a-miniport-driver"></a>ミニポート ドライバーからのデータの送信





次の図は、ミニポートドライバーの送信操作を示しています。

![ミニポートドライバーの送信操作を示す図](images/miniportsend.png)

NDIS は、ミニポートドライバーの[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数を呼び出して、ネットワークデータを転送します。この関数は、リンクされた[**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体のリストによって記述されています。

ミニポートドライバーは、 [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出して、NET\_バッファー\_リスト構造体のリンクリストをその後のドライバーに返し、送信要求の最終状態を返します。

 

 





