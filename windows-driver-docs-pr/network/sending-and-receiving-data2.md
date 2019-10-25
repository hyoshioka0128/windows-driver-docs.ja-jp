---
title: CoNDIS でのデータの送信と受信
description: CoNDIS でのデータの送信と受信
ms.assetid: aad7ccf9-0eaa-4327-b048-268d12593a70
keywords:
- 仮想接続 WDK、データ転送
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 339f0c8538eb2962e84ec502b338ec333eac6ac9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841978"
---
# <a name="sending-and-receiving-data-in-condis"></a>CoNDIS でのデータの送信と受信





データの転送には、確立されたアクティブな VC 経由でのパケットの送受信が含まれます。

**注**  プロトコルドライバーは、その Vc の[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)を呼び出した後、vc にデータを送信するために[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)を呼び出すことはできません。

 

CoNDIS send 関数と receive 関数は、コネクションレスの送信関数と受信関数に似ています。 CoNDIS コネクションレスインターフェイスの主な違いは、仮想接続 (VCs) の管理です。 コネクションレスの送信操作と受信操作の詳細については、「[送信および受信操作](send-and-receive-operations.md)」を参照してください。

1回の関数呼び出しでは、CoNDIS ドライバーは、各 NET\_BUFFER\_LIST 構造体に複数の[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を持つ複数の[**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を送信できます。 また、CoNDIS ドライバーは、各 NET\_BUFFER\_LIST 構造体に複数の NET\_バッファー構造を持つ複数の net\_BUFFER\_リスト構造に対して、完了した送信操作を示すことができます。

受信パスでは、CoNDIS ミニポートドライバーは、受信を示すために、NET\_BUFFER\_LIST 構造体の一覧を提供できます。 ミニポートドライバーに用意されている各 NET\_BUFFER\_リストには、1つの NET\_バッファー構造が含まれています。 異なるプロトコルバインドが各 NET\_BUFFER\_LIST 構造体を処理できるため、NDIS は各 NET\_BUFFER\_LIST 構造を個別にミニポートドライバーに返すことができます。

NDIS 5 をサポートします。*x*以前のドライバーは、レガシ[**NDIS\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造と NET\_バッファーベースの構造体の間に変換レイヤーを提供します。 CoNDIS は、NET\_バッファー構造と NDIS\_パケット構造との間で必要な変換を実行します。 変換によってパフォーマンスが低下しないようにするには、CoNDIS ドライバーを更新して、NET\_バッファー構造をサポートする必要があります。また、すべてのデータパスで、複数の NET\_バッファー\_リスト構造をサポートする必要があります。

ここでは、次のトピックについて説明します。

[CoNDIS ドライバーからの NET\_バッファー構造の送信](sending-net-buffer-structures-from-condis-drivers.md)

[CoNDIS での NET\_バッファー構造の受信](receiving-net-buffer-structures-in-condis-drivers.md)

 

 





