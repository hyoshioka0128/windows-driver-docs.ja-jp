---
title: CoNDIS WAN ミニポート ドライバーからのパケットの送信
description: CoNDIS WAN ミニポート ドライバーからのパケットの送信
ms.assetid: 66c42e90-e0d9-47d1-9e6d-cadb511bcb7a
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワー キング、パケットを送信します。
- ループバックする WDK ネットワーク
- ソフトウェアのループバックする WDK ネットワーク
- 無作為検出モード ループバックする WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dccd719b551a3f61a602c87475d9b6c4297a51d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386836"
---
# <a name="sending-packets-from-a-condis-wan-miniport-driver"></a>CoNDIS WAN ミニポート ドライバーからのパケットの送信





上位層、ドライバーは呼び出し[ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)に基になるのいる CoNDIS WAN ミニポート ドライバーの一覧でネットワーク データ パケットを送信する[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 NDISWAN 中間ドライバーが、転送、NET\_バッファー\_上位レイヤー ドライバーからリストの構造体。 NDISWAN では、構造体はそれらを送信する前にします。 NDISWAN 新しい NET でパケットを転送する\_バッファー\_リストの構造体。

NDISWAN 中間ドライバー呼び出し、新しい NET を転送するように NDIS\_バッファー\_リスト構造では、NDIS 呼び出し、WAN ミニポート ドライバーの[ **MiniportCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数。

いる CoNDIS WAN ミニポート ドライバーが両方、NET を所有している\_バッファー\_リストの構造体と、送信が完了するまで、関連付けられているデータ。 ミニポート ドライバーが後で呼び出す必要があります[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)送信要求を完了します。

完了コールバックが必ずしもネットワーク データが送信されました。ただし、インテリジェントな Nic を除くネットワークのデータは、通常は既に転送されました。 完了コールバックは、NET の所有権を解放する準備ができて、ミニポート ドライバーであることを示す\_バッファー\_リストの構造体。

後いる CoNDIS WAN ミニポート ドライバーで受信 NET\_バッファー\_ネットワーク データ パケットを含むリスト構造で、アクティブな接続 (VC) をパケットを送る。

いる CoNDIS WAN ミニポート ドライバーで VC あたりが保持できる未処理のパケットの数を指定する、 **MaxSendWindow**の NDIS メンバー\_WAN\_CO\_情報構造体。 ミニポート ドライバーに応答するときに、ミニポート ドライバーがこの構造体を提供します、 [OID\_WAN\_CO\_取得\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-info)プロトコル ドライバーからの要求。 ただし、ミニポート ドライバーと調整できますこの数に動的に VC あたりごとを使用して、 **SendWindow**内のメンバー、 [ **WAN\_CO\_LINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))構造体。 ミニポート ドライバーがこの構造体を渡す、 [ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)関数。 使用して、現在の NDISWAN **SendWindow**として未処理の送信の制限値。 ミニポート ドライバーの値を設定できる、 **SendWindow**未処理のパケットを処理できないことを指定する 0 にメンバー。 つまり場合、 **SendWindow**メンバーが 0 に設定されている、送信ウィンドウをシャット ダウンおよび NDISWAN が特定の VC のパケットの送信を停止します。

WAN ミニポート ドライバーに送信されるパケットは、単純な HDLC PPP フレームを含めることが PPP フレームが設定されている場合。 明細または RAS フレームでは、パケットには一切フレームと共にデータ部分のみが含まれません。 WAN のパケットのフレーミングの詳細については、次を参照してください。 [WAN パケットのフレーミング](wan-packet-framing.md)します。

WAN ミニポート ドライバーは、ソフトウェア ループバックまたは無作為検出モード ループバック提供を試みませんする必要があります。 両方のループバック型は完全に NDISWAN ドライバーがサポートされます。

 

 





