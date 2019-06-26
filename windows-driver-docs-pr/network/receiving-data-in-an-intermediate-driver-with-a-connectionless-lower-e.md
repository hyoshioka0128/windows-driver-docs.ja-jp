---
title: コネクションレス低い edge ドライバーの中間データの受信
description: コネクションレスの下端を含む中間ドライバーでのデータの受信
ms.assetid: 73143c2f-4127-41fc-b916-eac87521440a
keywords:
- 中間ドライバー WDK ネットワー キング、受信操作
- NDIS は、ドライバー WDK を中間、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4a27b35c2d56985126be44a9072d90782751c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368474"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connectionless-lower-edge"></a>コネクションレスの下端を含む中間ドライバーでのデータの受信





コネクションレスの下端と中間のドライバーが必要、 [ **ProtocolReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)ネットワーク データを受信する関数。

コネクションレスのミニポート ドライバーの呼び出しを基になる、 **NdisMIndicateReceiveNetBufferLists**、1 つ以上のリンクされたリストを渡すこと[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体より高いレベルのドライバーに示された構造体の所有権を放棄します。 NET を返すより高いレベルのドライバーのデータを使用すると、\_バッファー\_ミニポート ドライバーに構造体 (および指定したリソース) を一覧表示します。

コネクションレスの下端と中間のドライバーのデータの受信についての詳細については、次を参照してください。[プロトコル ドライバーの送信と受信操作](protocol-driver-send-and-receive-operations.md)します。

 

 





