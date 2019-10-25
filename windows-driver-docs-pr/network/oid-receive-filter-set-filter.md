---
title: OID_RECEIVE_FILTER_SET_FILTER
description: ネットワークアダプターにフィルターを設定するために、OID_RECEIVE_FILTER_SET_FILTER の OID メソッド要求が、後続のドライバーによって発行されます。
ms.assetid: ec3e119e-662f-48a6-8c68-20da20590b24
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_SET_FILTER ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: cf6848f8bccc829dcad2bb01c42e60469a76da73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843995"
---
# <a name="oid_receive_filter_set_filter"></a>OID\_受信\_フィルター\_設定\_フィルター

ネットワークアダプターにフィルターを設定する\_フィルター\_設定して、oid の OID メソッドの要求を送信すると、そのドライバーによって\_フィルターが\_されます。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、呼び出し元が割り当てたバッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   Ndis\_は、NDIS 受信フィルターのパラメーターを指定する[ **\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を受け取ります。

-   ネットワークパケットヘッダー内のフィールドのフィルターテスト条件を指定する、 [ **\_フィルター\_フィールド\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)の配列。

OID メソッド要求から正常に復帰した後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、ndis へのポインターが含まれています[ **\_\_パラメーターを受け取る\_フィルターを受け取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)ます。データ. それまでのドライバーが新しい受信フィルターを作成している場合、NDIS はこの構造を新しいフィルター識別子で更新します。

<a name="remarks"></a>注釈
-------

NDIS 受信フィルターは、次の NDIS インターフェイスで使用されます。

-   [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)」を参照してください。

-   [シングルルート I/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[仮想ポートでの受信フィルターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)」を参照してください。

-   [仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)」を参照してください。

OID\_受信\_フィルター\_\_設定の oid メソッド要求は、NDIS パケット合体、SR-IOV、または VMQ インターフェイスをサポートするミニポートドライバーでは必須です。

前のドライバーは、要求されたフィルター構成を使用して、 [ **\_フィルター\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)を初期化します。 NDIS によって、NDIS の**filterid**メンバーにフィルター識別子が割り当てられ、\_受信\_フィルター\_PARAMETERS 構造が割り当てられ、基になるミニポートドライバーにメソッド要求が渡されます。

受信キューに設定されている各フィルターには、ネットワークアダプターの一意のフィルター識別子があります。 つまり、フィルター識別子は、ネットワークアダプターが管理する別のキューでは複製されません。 NDIS が受信キューにフィルターを設定するための OID 要求を受信すると、フィルターパラメーターが検証されます。 NDIS によって必要なリソースとフィルター識別子が割り当てられると、基になるネットワークアダプターに OID 要求が送信されます。 ネットワークアダプターがフィルターに必要なソフトウェアリソースとハードウェアリソースを正常に割り当てることができる場合、NDIS\_STATUS\_SUCCESS の戻りステータスを持つ OID 要求を完了します。

**メモ** NDIS 6.30 以降では、パケット合体受信フィルターは、ネットワークアダプターの既定の受信キューでのみサポートされています。 この受信キューには、NDIS\_既定\_受信\_キュー\_ID の識別子が設定されています。



ミニポートドライバーは、割り当てられた受信フィルターのフィルター識別子を保持する必要があります。 NDIS は、後の OID 要求でフィルターの識別子を使用して受信フィルターパラメーターを変更するか、受信フィルターをクリアします。

ミニポートドライバーが\_OID を受信した後[\_フィルター\_キュー\_割り当て\_](oid-receive-filter-queue-allocation-complete.md)要求を完了し、キューに設定されたフィルターがある場合、キューは*実行中*の状態になります。 この状態では、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出すことによって、ミニポートドライバーがキュー内のパケットの兆候を開始できます。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>Sr-iov インターフェイスに関するその他のガイドライン

SR-IOV インターフェイスをサポートするミニポートドライバーには、次の点が適用されます。

-   SR-IOV インターフェイスの場合、受信キューは既定または既定以外の仮想ポート (VPort) で作成されます。

    **メモ** Windows Server 2012 以降では、SR-IOV インターフェイスは、VPort の既定の受信キューのみをサポートしています。

    Oid\_NIC\_スイッチの oid セット要求を通じて sr-iov VPort が割り当てられた後[\_vport を作成\_](oid-nic-switch-create-vport.md)と、それ以降のドライバーは、oid の oid 要求を使用して vport にフィルターを設定でき\_フィルター\_設定されます。\_フィルター。

    **メモ** VPort を割り当てた後のドライバーだけが、その VPort にフィルターを設定できます。

-   既定の VPort は常に存在するので、それまでのドライバーは常に既定の VPort にフィルターを設定できます。

-   VPort が作成されると、受信フィルターは設定されません。 この場合、ミニポートドライバーは、その VPort の受信パケットを示すことはできません。この場合、ミニポートドライバーは、VPort のフィルター\_フィルター\_設定された oid 要求を受信\_\_します。 この OID 要求が発行されると、ミニポートドライバーはその VPort 上のパケットを示すことができます。

    **メモ** ミニポートドライバーが oid の OID 要求を処理している間に VPort のパケットを示していて、\_フィルター\_設定された\_受信\_フィルターの場合、OID 要求を完了し、NDIS\_STATUS\_SUCCESS status code を返す必要があります。

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ インターフェイスに関する追加のガイドライン

VMQ インターフェイスをサポートするミニポートドライバーには、次の点が適用されます。

-   VMQ 受信キューが割り当てられると、その後のドライバーは、oid の OID 要求を使用して受信キューにフィルターを設定し、\_フィルター\_設定された\_受信\_フィルターを設定できます。

    **メモ** 受信キューを割り当てたプロトコルドライバーだけが、そのキューにフィルターを設定できます。

-   既定のキューは常に存在するので、それまでのドライバーは常に既定のキューにフィルターを設定できます。 ネットワークアダプターがドロップキューをサポートしている場合は、そのドライバーがドロップキューにフィルターを設定できます。

    後続のドライバーは、既定のキューまたはドロップキューを所有しません。 そのため、ネットワークアダプターにバインドされているすべてのプロトコルドライバーは、既定のキューまたはドロップキューを使用します。

-   受信キューが作成されると、受信フィルターは設定されません。 この場合、ミニポートドライバーは、受信キューの受信パケットを示すことはできません。この場合、ミニポートドライバーは、受信キューのフィルター\_設定\_フィルターを受信\_フィルターを使用して oid 要求を受信\_ます。 この OID 要求が発行されると、ミニポートドライバーはその受信キューのパケットを示すことができます。

    **メモ** Oid 要求を処理している間に、ミニポートドライバーが oid 要求を処理しているときにキューのパケットを示している場合は\_\_フィルター\_設定\_フィルターでは、OID 要求を完了し、NDIS\_STATUS\_SUCCESS status code を返す必要があります。

### <a name="return-status-codes"></a>ステータスコードを返す

ミニポートドライバーは、oid の OID メソッド要求について、次のいずれかの状態コードを返し\_フィルター\_設定された OID\_受信\_フィルターを設定します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
フィルターがキューに正常に設定されました。 情報バッファーには、更新された[**NDIS\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体が含まれています。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されます。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_の状態\_無効な\_パラメーターです  
指定された後続のドライバーが有効ではないパラメーターが1つ以上あります。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_の状態\_無効な\_の長さです  
情報バッファーが短すぎます。 NDIS はデータを設定**します。メソッド\_情報。** 必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーが必要です。

<a href="" id="ndis-status-not-supported"></a>NDIS\_の状態\_\_サポートされていません  
ミニポートドライバーの NDIS バージョンは、6.20 より前のバージョンです。

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
<td><p>NDIS 6.20 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_受信\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[**NET\_BUFFER\_LIST\_受信\_フィルター\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-id)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[OID\_受信\_フィルター\_クリア\_フィルター](oid-receive-filter-clear-filter.md)

[OID\_受信\_フィルター\_キュー\_割り当て\_完了](oid-receive-filter-queue-allocation-complete.md)