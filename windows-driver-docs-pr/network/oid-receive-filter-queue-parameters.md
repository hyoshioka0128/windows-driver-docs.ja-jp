---
title: OID_RECEIVE_FILTER_QUEUE_PARAMETERS
description: 後続のドライバーは、受信キューの現在の構成パラメーターを取得するために、OID_RECEIVE_FILTER_QUEUE_PARAMETERS のオブジェクト識別子 (OID) メソッドの要求を発行します。
ms.assetid: f6cd7896-0811-4029-b1d8-8cf800d7813e
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_QUEUE_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: e291b519fe6248f65238f320b75479b77717ac64
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843997"
---
# <a name="oid_receive_filter_queue_parameters"></a>OID\_\_フィルター\_\_キューのパラメーターを受け取る


後続のドライバーは、オブジェクト識別子 (OID) のメソッドの要求を OID\_受信\_フィルター\_キュー\_パラメーターを受け取って、受信キューの現在の構成パラメーターを取得します。 Ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、NDIS [ **\_RECEIVE\_queue\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)型のキュー識別子を持つパラメーター構造へのポインターが含まれてい **\_\_キュー\_ID を受信**します。 OID メソッド要求から正常に復帰した後、 **ndis\_oid\_要求**構造の**informationbuffer**メンバーには、 **ndis\_RECEIVE\_QUEUE\_パラメーター**へのポインターが含まれています。データ.

後続のドライバーは、OID の OID セット要求を発行し、キューの現在の構成パラメーターを変更するために、キュー\_パラメーターを受信\_フィルター\_\_します。 このドライバーは、ndis [ **\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバー内の[ **\_キュー\_パラメーターの構造を受け取る ndis\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)を指すポインターを提供します。

<a name="remarks"></a>注釈
-------

その後のドライバーは、OID の OID セット要求を発行\_、キュー\_パラメーターを\_\_受け取って1つ以上の受信キューのパラメーターを変更します。 OID セット要求は、NDIS 6.20 以降のミニポートドライバーでは省略可能です。 ただし、この OID 要求は、仮想マシンキュー (VMQ) インターフェイスをサポートするミニポートドライバーでは必須です。

**注**  、キューを割り当てた後のドライバーだけが、OID の oid セット要求を発行することによって構成パラメーターを変更できることに注意してください\_キュー\_パラメーター\_受信\_フィルター。

 

先行するドライバーは、以前の Oid からキュー識別子の入力値を取得し、\_QUEUE メソッド OID 要求を[割り当てる\_\_フィルターを受け取る\_](oid-receive-filter-allocate-queue.md)ます。

後続のドライバーによってキューが割り当てられた後、**フラグ**メンバーでは、対応する変更フラグ (NDIS\_RECEIVE\_QUEUE\_PARAMETER\_*Xxx*\_CHANGED) を持つ構成パラメーターを変更できます。[ **\_QUEUE\_PARAMETERS 構造体を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters) 。 ただし、キューが割り当てられた後、それ以降のドライバーは、対応する変更フラグが設定されていない構成パラメーターを変更することはできません。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、oid の OID メソッド要求を処理します。これは、ミニポートドライバーの\_パラメーターを受信\_フィルター\_キューに\_、次のいずれかのステータスコードを返します。

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
<td><p>要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>要求は完了待ちです。 NDIS は、要求が完了した後に、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが短すぎます。 NDIS は<strong>データ</strong>を設定します。<strong>METHOD_INFORMATION</strong>。NDIS_OID_REQUEST 構造体の中で必要とされる最小バッファーサイズに対して、 <strong>Bytesneeded 必要</strong>です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>基になるネットワークアダプターでサポートされていない機能を有効にしようとしたため、要求は失敗しました。</p></td>
</tr>
<tr class="odd">
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

[**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[OID\_受信\_フィルター\_割り当て\_キュー](oid-receive-filter-allocate-queue.md)

[OID\_\_フィルター\_\_キューのパラメーターを受け取る](oid-receive-filter-queue-parameters.md)

 

 




