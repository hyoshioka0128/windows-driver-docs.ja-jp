---
title: 接続指向のエッジ中間ドライバーデータの受信
description: 接続指向の下端を含む中間ドライバーでのデータの受信
ms.assetid: c14b4e8a-cfa2-4771-83b2-aa20fda79d39
keywords:
- 中間ドライバー WDK ネットワーク、受信操作
- NDIS 中間ドライバー WDK、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb707412114ecb42922c65bbb504288726df213a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844851"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connection-oriented-lower-edge"></a>接続指向の下端を含む中間ドライバーでのデータの受信





中間ドライバーが接続指向ミニポートドライバーの上にある場合、NDIS は、中間ドライバーの[**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)関数を呼び出して、受信したデータを示します。

基になる接続指向ミニポートドライバーは、 [**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)を呼び出してネットワークデータを示し、1つまたは複数の[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストを渡します。

接続指向の下端を持つ中間ドライバーでのデータの受信の詳細については、「[接続指向の操作](connection-oriented-operations.md)」を参照してください。

 

 





