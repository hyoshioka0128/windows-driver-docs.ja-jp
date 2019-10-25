---
title: 送信および受信操作
description: 送信および受信操作
ms.assetid: 216bfed2-92f8-4480-95fc-9909d7c1f533
keywords:
- ネットワークデータ WDK、送信
- ネットワークデータ WDK、受信
- データ WDK ネットワーク, 送信
- データ WDK ネットワーク、受信
- データの送信 (WDK ネットワーク)
- データを受信する WDK ネットワーク
- NET_BUFFER_LIST
- 複数の NET_BUFFER_LIST 構造の WDK networki
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02f562ef824766b0cf881c2fca4e399c1fba478d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841984"
---
# <a name="send-and-receive-operations"></a>送信および受信操作





1回の関数呼び出しでは、NDIS 6.0 ドライバーは、各 NET\_BUFFER\_LIST 構造体に複数の[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を持つ複数の[**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を送信できます。 また、NDIS ドライバーは、net\_BUFFER\_LIST 構造体に複数の NET\_バッファー構造を持つ複数の net\_BUFFER\_LIST 構造体に対して、完了した送信操作を示すことができます。

受信パスでは、ミニポートドライバーは、受信を示すために、NET\_BUFFER\_LIST 構造体の一覧を使用できます。 ミニポートドライバーによって示される各 NET\_BUFFER\_リストには、1つの NET\_バッファー構造が含まれています。 ただし、ネイティブ802.11 ドライバーは、複数の NET\_バッファー構造を持つことができます。 異なるプロトコルバインドが各 NET\_BUFFER\_LIST 構造体を処理できるため、NDIS は各 NET\_BUFFER\_LIST 構造を個別にミニポートドライバーに返すことができます。

NDIS 5 をサポートします。バージョン*x*以前のドライバーは、NDIS [ **\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))ベースのインターフェイスと NET\_のバッファーベースのインターフェイスとの間に変換レイヤーを提供します。 NDIS は、 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造と NDIS\_パケット構造との間で必要な変換を実行します。 変換によるパフォーマンスの低下を回避するには、NDIS ドライバーを更新して、NET\_バッファー構造を使用し、すべてのデータパスで複数の[**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造をサポートする必要があります。

ここでは、次のトピックについて説明します。

[ネットワークデータの送信](sending-network-data.md)

[送信操作の取り消し](canceling-a-send-operation.md)

[ネットワークデータの受信](receiving-network-data.md)

[NDIS パケットのループバック](looping-back-ndis-packets.md)

 

 





