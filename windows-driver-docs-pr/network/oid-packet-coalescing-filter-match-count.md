---
title: OID_PACKET_COALESCING_FILTER_MATCH_COUNT
description: NDIS は、キャッシュ、または 1 つにまとめ、ネットワーク アダプターのされたパケットの数を取得する OID_PACKET_COALESCING_FILTER_MATCH_COUNT の OID クエリ要求を発行します。
ms.assetid: 3325865D-A329-4562-8270-CC2F42043D48
ms.date: 08/08/2017
keywords: -OID_PACKET_COALESCING_FILTER_MATCH_COUNT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0d36c0cd0b56e6697748a9bd47dabc257b72406d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383247"
---
# <a name="oidpacketcoalescingfiltermatchcount"></a>OID\_パケット\_COALESCING\_フィルター\_一致\_数


OID の OID クエリ要求を発行する NDIS\_パケット\_COALESCING\_フィルター\_一致\_キャッシュされたパケットの数を取得する数または*まとめられた*のネットワーク アダプター。 アダプターが有効な場合、ネットワーク アダプターが受信したパケットを連結[NDIS パケット結合](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)パケットが受信フィルターに一致するとします。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には、呼び出し元が割り当てた ULONG64 変数へのポインターが含まれています. クエリ要求から正常に返された前に、ドライバー更新プログラム、ULONG64 変数に一致したパケットの数とは、ネットワーク アダプターのフィルターを受信します。

<a name="remarks"></a>コメント
-------

NDIS 6.30、以降をサポートするドライバー [NDIS パケット結合](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)OID の OID クエリ要求をサポートする必要があります\_パケット\_COALESCING\_フィルター\_一致\_カウントします。

**注**  をサポートするドライバー、[シングル ルート I/O 仮想化 (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)または[仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)インターフェイスは、OID クエリ要求をサポートする必要はありませんこの OID。

 

パケットの結合をサポートしているミニポート ドライバーでは、各ネットワーク アダプターで結合された受信パケットの ULONG64 カウンターをインクリメントする必要があります。 上にあるどのドライバーのダウンロードの OID メソッド要求を通じたミニポート ドライバーに、受信フィルターに一致した場合、パケットが結合された[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md).

ドライバーが、OID の OID のクエリ要求を処理する場合、このカウンターの値を返します\_パケット\_COALESCING\_フィルター\_一致\_数。

OID の OID のクエリ要求を処理した後、ミニポート ドライバー、カウンターをクリアする必要があります\_パケット\_COALESCING\_フィルター\_一致\_数。 次の条件に該当する場合、ミニポート ドライバーは、カウンターをオフだけする必要があります。

-   ミニポート ドライバーの OID セット要求を処理する[OID\_PNP\_設定\_POWER](oid-pnp-set-power.md) NdisDeviceStateD0 の電力状態に再開します。

-   NDIS ミニポート ドライバーの呼び出す[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)関数を基になるネットワーク アダプターをリセットします。

パケットの結合の詳細については、次を参照してください。 [NDIS パケット結合](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_パケット\_COALESCING\_フィルター\_一致\_数。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
OID 要求は正常に完了しました。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状態\_無効な\_長さ  
情報バッファーが小さすぎます。 ドライバーのセット、**データ。設定\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体に必要な最小バッファー サイズ。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
他の理由から、要求が失敗しました。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[OID\_PNP\_設定\_電源](oid-pnp-set-power.md)

[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)

 

 




