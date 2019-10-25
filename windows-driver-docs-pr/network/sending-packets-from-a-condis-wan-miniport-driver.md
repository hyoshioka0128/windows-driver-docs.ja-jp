---
title: CoNDIS WAN ミニポート ドライバーからのパケットの送信
description: CoNDIS WAN ミニポート ドライバーからのパケットの送信
ms.assetid: 66c42e90-e0d9-47d1-9e6d-cadb511bcb7a
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、パケット送信
- ループバックを WDK ネットワーク
- software ループバックを WDK ネットワーク
- 無作為検出-モードループバックを WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07bbad0de67fd1413188334737aa73e1b882c8ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841956"
---
# <a name="sending-packets-from-a-condis-wan-miniport-driver"></a>CoNDIS WAN ミニポート ドライバーからのパケットの送信





上層のドライバーは、 [**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)を呼び出して、ネットワークデータパケットを、 [**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の一覧にある基になる condis WAN ミニポートドライバーに送信します。 NDISWAN 中間ドライバーは、これらの NET\_バッファー\_リスト構造を上位層ドライバーから転送します。 NDISWAN を送信する前に構造体を再パッケージ化します。 NDISWAN は、新しい NET\_BUFFER\_LIST 構造体にパケットを転送します。

NDISWAN 中間ドライバーは、NDIS を呼び出して新しい NET\_BUFFER\_LIST 構造体を転送し、NDIS は WAN ミニポートドライバーの[**Miniportcosendnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数を呼び出します。

CoNDIS WAN ミニポートドライバーは、送信が完了するまで、NET\_BUFFER\_LIST 構造体と関連データの両方を所有します。 ミニポートドライバーは、後で[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)を呼び出して送信要求を完了する必要があります。

完了呼び出しでは、必ずしもネットワーク datahas 送信されたことを示しているわけではありません。ただし、インテリジェントな Nic を除き、通常、ネットワークデータは送信されています。 ただし、完了呼び出しでは、ミニポートドライバーが NET\_バッファー\_リスト構造の所有権を解放する準備ができていることを示しています。

CoNDIS WAN ミニポートドライバーがネットワークデータパケットを含む NET\_BUFFER\_LIST 構造を受け取ると、アクティブな仮想接続 (VC) にパケットを送信する必要があります。

CoNDIS WAN ミニポートドライバーは、NDIS\_WAN\_CO\_INFO 構造体の**Maxsendwindow**メンバーの VC ごとに保持できる未処理のパケットの数を指定します。 ミニポートドライバーは、ミニポートドライバーが OID に応答するときにこの構造を提供し[\_WAN\_CO\_GET\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-info)要求をプロトコルドライバーから取得します。 ただし、ミニポートドライバーは、 [**WAN\_CO\_LINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))構造の**sendwindow**メンバーを使用して、この数を VC 単位で動的に調整できます。 ミニポートドライバーは、この構造体を[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)関数に渡します。 NDISWAN は、現在の**Sendwindow**の値を未処理の送信の制限として使用します。 ミニポートドライバーは、 **Sendwindow**メンバーの値を0に設定して、未処理のパケットを処理できないことを指定できます。 つまり、 **sendwindow**メンバーが0に設定されている場合、送信ウィンドウはシャットダウンされ、NDISWAN は特定の VC のパケットの送信を停止します。

WAN ミニポートドライバーから送信されるパケットは、PPP フレームが設定されている場合、単純な HDLC PPP フレーミングを含みます。 SLIP または RAS フレーミングの場合、パケットには、データ部分のみが含まれ、フレームはまったくありません。 WAN パケットフレーミングの詳細については、「 [Wan パケットフレーム](wan-packet-framing.md)」を参照してください。

WAN ミニポートドライバーは、ソフトウェアループバックまたは無作為検出モードのループバックを提供しないようにする必要があります。 これらのループバックの種類はいずれも、NDISWAN ドライバーによって完全にサポートされています。

 

 





