---
title: OID_RECEIVE_FILTER_ALLOCATE_QUEUE
description: 後続のドライバーは、構成パラメーターの初期セットを持つキューを割り当てるために、OID_RECEIVE_FILTER_ALLOCATE_QUEUE のオブジェクト識別子 (OID) メソッドの要求を発行します。
ms.assetid: 8dd7ab91-b752-46fd-ae1b-014dc0fb0157
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_RECEIVE_FILTER_ALLOCATE_QUEUE
ms.localizationpriority: medium
ms.openlocfilehash: 523504240dbf551be331bceccd6c8d8e4ff851a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844021"
---
# <a name="oid_receive_filter_allocate_queue"></a>OID\_受信\_フィルター\_割り当て\_キュー


後続のドライバーは、オブジェクト識別子 (OID) メソッドの OID の要求を発行\_受信\_フィルター\_\_キューを割り当てて、構成パラメーターの初期セットを持つキューを割り当てます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体へのポインターが含まれています。 OID メソッド要求から正常に戻った後、 **ndis\_oid\_要求**構造の**informationbuffer**メンバーには、新しいキュー識別子を持つ**ndis\_RECEIVE\_queue\_PARAMETERS**構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

\_キューの割り当て\_\_フィルターを受け取る oid\_oid メソッドの要求は、NDIS 6.20 以降のミニポートドライバーでは省略可能です。 バーチャルマシンキュー (VMQ) インターフェイスをサポートするミニポートドライバーでは必須です。

前のドライバーは、要求されたキュー構成を使用して、 [ **\_キュー\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)を初期化します。 NDIS は、Ndis の**Queueid**メンバーにキュー識別子を割り当て、 **\_queue\_PARAMETERS 構造体\_受信**し、そのメソッド要求をミニポートドライバーに渡します。

このような場合は、 **\_キュー\_パラメーター**を受け取るように[ **、ndis を**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)\_設定できます。**これ  、** \_キュー\_受信\_キューに\_を受信\_パラメーターを受け取る\_、\_の\_を受信\_\_の**フラグ**のメンバーで\_**必要な**フラグを\_\_受信に渡す必要があります。 その他のフラグは、キューの割り当てには使用されません。

 

ミニポートドライバーが oid 要求を発行した後、\_キューの割り当て\_\_フィルターを受信\_、正常に処理されると、キューは一時停止状態になります。

その後のドライバーでは、その後の OID 要求で NDIS が提供するキュー識別子を使用する必要があります。たとえば、キューパラメーターを変更したり、キューを解放したりできます。 キュー id は、キューに関連付けられているすべての[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の帯域外 (OOB) データにも含まれます。 ドライバーは、net [ **\_buffer\_list\_受信\_queue\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)マクロを使用して、 **net\_buffer\_LIST**構造体のキュー識別子を取得します。

NDIS は、受信キューの割り当てに OID 要求を受信すると、キューパラメーターを確認します。 NDIS によって必要なリソースとキュー識別子が割り当てられると、基になるミニポートドライバーに OID 要求が送信されます。 キュー識別子は、関連付けられているネットワークアダプターに対して一意です。

ミニポートドライバーが受信キューに必要なソフトウェアおよびハードウェアリソースを正常に割り当てることができる場合、 **NDIS\_STATUS\_SUCCESS**を返すことによって OID 要求を完了します。

ミニポートドライバーは、割り当てられた受信キューのキュー識別子を保持する必要があります。 NDIS では、受信キューのキュー識別子を使用して、受信キューに受信フィルターを設定したり、受信キューパラメーターを変更したり、受信キューを解放したりします。

1つ以上の受信キューが割り当てられた後、必要に応じて初期フィルターを設定した後は、Oid を発行して、受信キューの現在のバッチに対する割り当てが完了したことをミニポートドライバーに通知するために、oid 要求の[受信\_フィルター\_キュー\_\_割り当てを\_](oid-receive-filter-queue-allocation-complete.md)必要があります。

そのキューにフィルターが設定されていない場合、ミニポートドライバーは受信キューにあるパケットを保持しないようにする必要があります。 キューにフィルターが設定されていないか、すべてのフィルターがオフになっている場合は、キューを空にして、すべてのパケットを破棄する必要があります。 つまり、パケットはドライバースタックに示されず、キューに保持されません。

それまでのドライバーは oid 要求を使用して、 [\_フィルター\_空き\_キューを受信](oid-receive-filter-free-queue.md)し、割り当てたキューを解放\_ます。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS またはミニポートドライバーは、oid の OID メソッドの要求について、次のいずれかの状態コードを返します\_フィルターを使用して\_キューを割り当てる\_\_ます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>キューが正常に割り当てられました。 情報バッファーには、更新された<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)"><strong>NDIS_RECEIVE_QUEUE_PARAMETERS</strong></a>構造が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>要求は完了待ちです。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>指定された1つ以上のパラメーターが有効ではありませんでした。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが短すぎます。 NDIS は<strong>データ</strong>を設定します。<strong>METHOD_INFORMATION</strong>。<strong>Bytesneeded</strong>必要な最小バッファーサイズに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>構造体のメンバーが必要です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>ミニポートドライバーの NDIS バージョンは、バージョン6.20 より前です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>他の理由で要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

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

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[**NET\_BUFFER\_LIST\_RECEIVE\_QUEUE\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)

[OID\_受信\_フィルター\_空き\_キュー](oid-receive-filter-free-queue.md)

[OID\_受信\_フィルター\_キュー\_割り当て\_完了](oid-receive-filter-queue-allocation-complete.md)

[**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

 

 




