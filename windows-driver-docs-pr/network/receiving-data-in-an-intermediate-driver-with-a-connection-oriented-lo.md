---
title: 下のエッジ中間ドライバーのデータ受信を接続指向
description: 接続指向の下端を含む中間ドライバーでのデータの受信
ms.assetid: c14b4e8a-cfa2-4771-83b2-aa20fda79d39
keywords:
- 中間ドライバー WDK ネットワー キング、受信操作
- NDIS は、ドライバー WDK を中間、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09bae2f773b1c4ce256f477531cb33e364822fc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373320"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connection-oriented-lower-edge"></a>接続指向の下端を含む中間ドライバーでのデータの受信





NDIS を呼び出して、中間のドライバーの場合は、中間ドライバーは、接続指向のミニポート ドライバー上に重ねられる、 [ **ProtocolCoReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)を受信したデータを示す関数。

基になる接続指向のミニポート ドライバーを呼び出すことでネットワーク データを示します[ **NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)、1 つまたは複数のリンク リストを渡して[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

接続指向の下端と中間のドライバーのデータの受信についての詳細については、次を参照してください。 [Connection-Oriented 操作](connection-oriented-operations.md)します。

 

 





