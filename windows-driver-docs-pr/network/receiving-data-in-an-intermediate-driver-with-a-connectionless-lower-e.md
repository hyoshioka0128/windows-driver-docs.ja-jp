---
title: コネクションレスエッジ中間ドライバーデータの受信
description: コネクションレスの下端を含む中間ドライバーでのデータの受信
ms.assetid: 73143c2f-4127-41fc-b916-eac87521440a
keywords:
- 中間ドライバー WDK ネットワーク、受信操作
- NDIS 中間ドライバー WDK、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00cfa34adc8f1f8d724747f069371c3eb6762558
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844849"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connectionless-lower-edge"></a>コネクションレスの下端を含む中間ドライバーでのデータの受信





ネットワークデータを受信するには、低速エッジがある中間ドライバーに[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数が必要です。

基になるコネクションレスなミニポートドライバーは、 **NdisMIndicateReceiveNetBufferLists**を呼び出し、1つ以上の[**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストを渡し、指定された構造体の所有権を上位に保っままします。レベルドライバー。 上位レベルのドライバーがデータを使用した場合は、NET\_BUFFER\_LIST 構造体 (および指定したリソース) がミニポートドライバーに返されます。

コネクションレスの低いエッジを使用して中間ドライバーでデータを受信する方法の詳細については、「[プロトコルドライバーの送信および受信操作](protocol-driver-send-and-receive-operations.md)」を参照してください。

 

 





