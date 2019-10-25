---
title: OID_RECEIVE_FILTER_CLEAR_FILTER
description: これまでのドライバーは、ネットワークアダプターの受信フィルターをクリアするために、OID_RECEIVE_FILTER_CLEAR_FILTER の OID セット要求を発行します。
ms.assetid: 5e92a11a-468e-431d-b4e5-7b0da3847e8a
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_CLEAR_FILTER ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: b5f9791eca2fbabaac7db3b92aa75fc49a9dcdf3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844019"
---
# <a name="oid_receive_filter_clear_filter"></a>OID\_受信\_フィルター\_クリア\_フィルター


それより後のドライバーは、OID の OID セット要求を発行して\_受信\_\_フィルターを適用して、ネットワークアダプターの受信フィルターをクリア\_フィルターをクリアします。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_FILTER\_CLEAR\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS 受信フィルターは、次の NDIS インターフェイスで使用されます。

-   [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)」を参照してください。

-   [シングルルート I/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[仮想ポートでの受信フィルターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)」を参照してください。

-   [仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)」を参照してください。

Oid パケット合体、SR-IOV、または VMQ インターフェイスをサポートするミニポートドライバーでは、oid の OID set 要求\_フィルター\_クリア\_フィルターを\_受信する必要があります。

前のドライバー (NDIS プロトコルやフィルタードライバーなど) では、OID\_受信\_フィルター\_クリア\_フィルターセット要求を使用して、以前に設定されたフィルターをクリアします。 受信フィルターを設定したドライバーだけがクリアされます。

前のドライバーでは、NDIS の**Filterid**メンバーを設定することによって受信フィルターをクリアします。これにより、 [ **\_パラメーター構造のクリア\_\_フィルターの\_が**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)フィルターの識別子に設定されます。 ドライバーは、以前の OID メソッドの Oid 要求からフィルター識別子を取得し、 [\_フィルター\_設定された\_受信\_フィルター](oid-receive-filter-set-filter.md)を取得します。

### <a name="additional-instructions-for-ndis-packet-coalescing"></a>NDIS パケット合体の追加手順

次の点は、NDIS パケット合体をサポートするミニポートおよびそれ以降のドライバーに適用されます。

-   ドライバーがバインド解除される前、またはドライバーから切断される前に、ミニポートドライバーに設定されているすべての受信フィルターを消去する必要があります。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>Sr-iov インターフェイスに関するその他のガイドライン

SR-IOV インターフェイスをサポートするミニポートおよびそれ以降のドライバーには、次の点が適用されます。

-   前のドライバーでは、VPort を解放する前に、SR-IOV VPort に設定されているすべてのフィルターをクリアする必要があります。 このドライバーは、ネットワークアダプターへのバインドを閉じる前に、既定の VPort に設定されているすべてのフィルターをクリアする必要があります。

-   ミニポートドライバーは、非既定の VPort のパケットを示す必要があります (oid の OID 要求が完了している場合)\_受信\_フィルター\_クリア\_フィルターを選択して、VPort の最後のフィルターをクリアします。

    また、ミニポートドライバーが oid 要求を完了している場合は、非既定の VPort のパケットを示す必要が**あり  ** [\_NIC\_スイッチ\_\_VPORT を削除](oid-nic-switch-delete-vport.md)して、vport を解放します。

     

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ インターフェイスに関する追加のガイドライン

次の点は、VMQ インターフェイスをサポートするミニポートおよびそれ以降のドライバーに適用されます。

-   後続のドライバーは、キューを解放する前に、VMQ 受信キューに設定されているすべてのフィルターをクリアする必要があります。 また、このドライバーは、ネットワークアダプターへのバインドを閉じる前に、既定のキューまたはドロップキューに設定されているすべてのフィルターをクリアする必要があります。

-   \_受信キューの最後のフィルターをクリアするには\_フィルターをクリア\_フィルターをオフにして、oid の OID 要求を完了したときに、ミニポートドライバーで受信キューのパケットを示すことはできません\_。

    また、ミニポートドライバーが oid 要求の oid 要求を完了している場合は、受信キューにあるパケットを示すこともできません\_受信キューを解放するには[\_フィルター\_無料\_キュー](oid-receive-filter-free-queue.md) **を  し**ます。

     

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数は、この要求に対して次のいずれかの値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>ミニポートドライバーが要求を正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポートドライバーは、要求を非同期的に完了します。 ミニポートドライバーはすべての処理を完了した後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>関数を呼び出し、 <em>STATUS</em>パラメーターに<strong>NDIS_STATUS_SUCCESS</strong>を渡すことによって、要求を成功させる必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポートアダプターが突然削除されています。</p></td>
</tr>
</tbody>
</table>

 

NDIS は、この要求に対して次のいずれかの状態コードを返します。

<a href="" id="ndis-status-success"></a>**NDIS\_状態\_成功**  
指定されたフィルターが正常にクリアされました。

<a href="" id="ndis-status-pending"></a>**NDIS\_状態\_保留中**  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-file-not-found"></a>**NDIS\_状態\_ファイル\_見つかりませ\_んでした**  
フィルター識別子が無効です。

<a href="" id="ndis-status-invalid-length"></a>**NDIS\_の状態\_無効な\_の長さです**  
情報バッファーが小さすぎます。 NDIS はデータを設定**します。\_情報を設定します。** 必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーが必要です。

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
<td><p>NDIS 6.20 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_\_パラメーターをクリア\_\_フィルターを受け取る**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)

[OID\_NIC\_スイッチ\_削除\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_受信\_フィルター\_空き\_キュー](oid-receive-filter-free-queue.md)

[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)

 

 




