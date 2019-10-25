---
title: ミニポート ドライバーからの受信データの表示
description: ミニポート ドライバーからの受信データの表示
ms.assetid: da5d31e9-5212-4c6c-bac2-81432a46c303
keywords:
- データを受信する WDK ネットワーク
- NdisMIndicateReceiveNetBufferLists
- indicatings WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5684ae3e1d6ecd0d4a454e8f77536308ad7306f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824625"
---
# <a name="indicating-received-data-from-a-miniport-driver"></a>ミニポート ドライバーからの受信データの表示





次の図は、ミニポートドライバーの受信通知を示しています。

![ミニポートドライバーの受信通知を示す図](images/miniportreceive.png)

ミニポートドライバーは、ネットワークからのデータの受信を示すために[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を呼び出します。 **NdisMIndicateReceiveNetBufferLists**関数は、指定された一連の[**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を、スタックの上位のドライバーに渡します。

ミニポートドライバーが、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)の*receiveflags*パラメーターで **\_FLAGS\_RESOURCES**フラグを受け取るように NDIS\_設定している場合、これは、ミニポートドライバーがの所有権を取り戻す必要があることを示します。[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をすぐに表示します。 この場合、NDIS はミニポートドライバーの[*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)関数を呼び出して、 **NET\_BUFFER\_LIST**構造体を返しません。 **NdisMIndicateReceiveNetBufferLists**が返された直後に、ミニポートドライバーは所有権を取得します。

ミニポートドライバーが、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)の*receiveflags*パラメーターで **\_FLAGS\_RESOURCES**フラグを受け取るように ndis\_設定していない場合、ndis は、指定された[**NET\_バッファーを返し\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)は、ミニポートドライバーの[*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)関数に構造体をリストします。 この場合、ミニポートドライバーは、NDIS が*Miniportreturnnetbufferlists*に戻るまで、指定された構造体の所有権を放棄します。

 

 





