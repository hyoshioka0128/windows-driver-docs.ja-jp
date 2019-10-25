---
title: OID_PACKET_COALESCING_FILTER_MATCH_COUNT
description: NDIS は、OID_PACKET_COALESCING_FILTER_MATCH_COUNT の OID クエリ要求を発行して、ネットワークアダプターでキャッシュまたは結合されたパケットの数を取得します。
ms.assetid: 3325865D-A329-4562-8270-CC2F42043D48
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_PACKET_COALESCING_FILTER_MATCH_COUNT ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 8e3cee607f632cebe14ac4b508106e2de71cc88d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844071"
---
# <a name="oid_packet_coalescing_filter_match_count"></a>OID\_パケット\_結合\_フィルター\_一致する\_カウント


NDIS は oid\_パケット\_結合\_\_\_フィルターの OID クエリ要求を発行して、ネットワークアダプター上でキャッシュされた (または*結合*された) パケットの数を取得します。 アダプターで[NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)が有効になっていて、パケットが受信フィルターと一致する場合、ネットワークアダプターは受信パケットを結合します。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、呼び出し元が割り当てた ULONG64 変数へのポインターが含まれています。 クエリ要求から正常に復帰する前に、ドライバーは ULONG64 変数を、ネットワークアダプター上で受信フィルターに一致したパケット数で更新します。

<a name="remarks"></a>注釈
-------

Ndis 6.30 以降では、 [ndis パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)をサポートするドライバーは、OID\_パケット\_結合\_フィルター\_一致する oid クエリ要求をサポートする必要があり\_カウントします。

**注  :** [シングルルート i/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)または[仮想マシンキュー (VMQ](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20) ) インターフェイスをサポートするドライバーは、この oid の oid クエリ要求をサポートするために必要ありません。

 

パケット合体をサポートするミニポートドライバーは、ネットワークアダプターで結合された受信パケットごとに ULONG64 カウンターを増やす必要があります。 パケットは受信フィルターに一致した場合に結合されます。このフィルター [\_設定された\_フィルターを受け取る\_フィルター設定さ](oid-receive-filter-set-filter.md)れている\_oid の oid メソッド要求を使用して、そのドライバーがミニポートドライバーにダウンロードされます。

このドライバーが oid クエリ要求を処理するときに、このカウンターの値が返されます。これは、OID\_パケット\_結合\_フィルター\_\_カウントに一致します。

\_パケット\_の oid クエリ要求を処理した後に、ミニポートドライバーがこのカウンターをクリアしないようにする必要があります。\_フィルター\_、\_カウントに一致します。 ミニポートドライバーは、次の条件に該当する場合にのみカウンターをクリアする必要があります。

-   ミニポートドライバーは oid\_PNP の OID セット要求を処理します。これにより、NdisDeviceStateD0 のフルパワー状態に復帰[\_電力が\_設定](oid-pnp-set-power.md)されます。

-   NDIS は、ミニポートドライバーの[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数を呼び出して、基になるネットワークアダプターをリセットします。

パケット合体の詳細については、「 [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーは、oid\_パケット\_結合\_フィルターの OID メソッド要求について、次のいずれかの状態コードを返し\_カウント\_します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
OID 要求が正常に完了しました。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_の状態\_無効な\_の長さです  
情報バッファーが短すぎます。 ドライバーはデータを設定し**ます。\_情報を設定します。** 必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーが必要です。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
他の理由で要求が失敗しました。

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
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_PNP\_設定\_電源](oid-pnp-set-power.md)

[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)

 

 




