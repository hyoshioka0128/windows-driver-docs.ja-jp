---
title: 接続指向ミニポート ドライバーのクエリ
description: 接続指向ミニポート ドライバーのクエリ
ms.assetid: 9e9926f6-cf90-48af-885f-59725721948d
keywords:
- 接続指向ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0704eeca1ee5ce7934a26a951a62014c3eefa2df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844903"
---
# <a name="querying-a-connection-oriented-miniport-driver"></a>接続指向ミニポート ドライバーのクエリ





接続指向のミニポートドライバーによって保持される情報オブジェクトを照会するために、バインドされたプロトコルは[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出し、クエリ対象のオブジェクト (oid) を指定する[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を渡します。とは、要求された情報を NDIS が最終的に書き込むバッファーを提供します。 **NdisCoOidRequest**を呼び出すと、ndis は、要求された情報を ndis に返すミニポートドライバーの[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を呼び出します。 *MiniportCoOidRequest*は、 [**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)の呼び出しを使用して同期的または非同期的に完了できます。

また、NDIS はミニポートドライバーの[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数を独自の方法で呼び出すこともできます。たとえば、ミニポートドライバーの[*MINIPORTINITIALIZEEX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から ndis\_STATUS\_が返された後に、ミニポートに対してクエリを実行します。ドライバーの機能、状態、または統計情報。 次の図は、接続指向ミニポートドライバーを照会する方法を示しています。

![接続指向ミニポートドライバーのクエリを示す図](images/fig5-3.png)

接続指向のミニポートドライバーは、特定の NIC のすべての仮想接続 (VCs) について、また VC ごとに、グローバルな情報を提供できる必要があります。 たとえば、 [OID\_GEN\_CO\_RCV\_crc\_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-rcv-crc-error)のクエリに対して**NULL**以外の*NdisVcHandle*を[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)に渡すと、ミニポートドライバーは crc エラーの数を返します。指定された VC でのすべての受信で発生した。 同じ要求に対して、 *NdisVcHandle*が NULL の場合、ミニポートドライバーは、NIC 経由で受信したすべての受信で発生した CRC エラーの合計数を返します。

次の一覧には、接続指向ミニポートドライバーに必要な一般的な操作 Oid のセットが含まれています。

[OID\_GEN\_共同\_サポートされている\_リスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-supported-list)

[OID\_GEN\_CO\_ハードウェア\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-hardware-status)

[OID\_GEN\_CO\_メディア\_サポートされています](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-media-supported)

[OID\_GEN\_CO\_メディア\_を使用して\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-media-in-use)

[OID\_GEN\_CO\_リンク\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-link-speed)

[OID\_GEN\_共同\_ベンダ\_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-vendor-id)

[OID\_GEN\_共同\_ベンダ\_説明](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-vendor-description)

[OID\_GEN\_CO\_ベンダ\_DRIVER\_バージョン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-vendor-driver-version)

[OID\_GEN\_CO\_DRIVER\_バージョン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-driver-version)

[OID\_GEN\_CO\_MAC\_オプション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-mac-options)

[OID\_GEN\_CO\_メディア\_接続\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-media-connect-status)

[OID\_GEN\_CO\_最小\_リンク\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-minimum-link-speed)

ミニポートドライバーの[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数は、必要に応じて、上記の oid に応答するように準備する必要があります。

[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)が OID\_GEN\_CO\_MAC\_オプションを使用して呼び出されると、ミニポートドライバーが実行するオプションの操作を指定するビットマスクを返す必要があります。 フラグのセットには、次のものが含まれます。

-   NDIS\_MAC\_オプション\_\_ループバックはありません。 このフラグが設定されている場合、ミニポートドライバーは、同じコンピューター上の受信者に送信される[**Miniportcosendnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)に渡されるパケットをループバックしません。また、ミニポートドライバーでは、NDIS がループバックを実行することを想定しています。 NDIS がパケットのループバックを実行する場合、パケットはミニポートドライバーに渡されません。 ミニポートドライバーは、NIC がハードウェアループバックをを実行しない限り、常にこのフラグを設定します。

-   NDIS\_MAC\_ETOX\_示されています。 このフラグが設定されている場合、ミニポートドライバーは、NIC がパケットを送信した後にのみ、送信が完了することを示します。

ミニポートドライバーでは、ndis\_MAC\_オプション\_予約フラグが使用されないようにする必要があります。このフラグは、NDIS 内部で使用するために予約されています。

また、 [*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)は、メディア固有の OID を使用してクエリを実行し、NIC の現在のアドレスを特定します。

詳細については、「[接続指向コールマネージャーとクライアントの oid](https://docs.microsoft.com/windows-hardware/drivers/network/oids-for-connection-oriented-call-managers-and-clients) 」と「[一般的なオブジェクト](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))」を参照してください。

 

 





