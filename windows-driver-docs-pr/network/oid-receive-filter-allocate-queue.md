---
title: OID_RECEIVE_FILTER_ALLOCATE_QUEUE
description: 上にあるドライバーは、オブジェクト識別子 OID_RECEIVE_FILTER_ALLOCATE_QUEUE の構成パラメーターの最初のセットを持つキューの割り当てを (OID) のメソッドを要求を発行します。
ms.assetid: 8dd7ab91-b752-46fd-ae1b-014dc0fb0157
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_ALLOCATE_QUEUE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 625123723d3d6899ab4817c46afee330b64ad4d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373328"
---
# <a name="oidreceivefilterallocatequeue"></a>OID\_受信\_フィルター\_ALLOCATE\_キュー


上にあるドライバーは、オブジェクト識別子の OID (OID) メソッドの要求を発行\_受信\_フィルター\_ALLOCATE\_を割り当てる、初期構成パラメーターのセットを含むキューのキュー。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造体にはへのポインターが含まれています、 **NDIS\_受信\_キュー\_パラメーター**新しいキューの識別子を持つ構造体。

<a name="remarks"></a>注釈
-------

OID の OID メソッド要求\_受信\_フィルター\_ALLOCATE\_キューは NDIS 6.20 が動作し、それ以降のミニポート ドライバーの省略可能です。 仮想マシン キュー (VMQ) インターフェイスをサポートするミニポート ドライバーに対して必要があります。

上にあるドライバーを初期化します、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)要求キューの構成を含む構造体。 NDIS キュー識別子を割り当てます、 **QueueId**のメンバー、 **NDIS\_受信\_キュー\_パラメーター**構造体、メソッド要求を渡すと、ミニポート ドライバー。

**注**  上にあるドライバーを設定できる、 **NDIS\_受信\_キュー\_パラメーター\_1 秒あたり\_キュー\_受信\_INDICATION**と**NDIS\_受信\_キュー\_パラメーター\_先読み\_分割\_REQUIRED**フラグ**フラグ**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体。 その他のフラグは、キューの割り当ては使用されません。

 

ミニポート ドライバーの OID、OID 要求が発行されると\_受信\_フィルター\_ALLOCATE\_キューとハンドルが正常にキューが一時停止状態にします。

上にあるドライバーは、キュー パラメーターを変更またはキューを解放するなど、NDIS が提供、OID の後続の要求でキューの id を使用する必要があります。 キューの id はすべてのアウト オブ バンド (OOB) データにも含まれています。 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)キューに関連付けられている構造体。 ドライバーを使用して、 [ **NET\_バッファー\_一覧\_受信\_キュー\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id) でキューのidを取得するマクロ**NET\_バッファー\_一覧**構造体。

NDIS は、受信キューを割り当てる OID 要求を受信、キューのパラメーターを確認します。 NDIS は、必要なリソースとキューの id を割り当て後、は、基になるミニポート ドライバーに OID 要求を送信します。 キューの id は、関連付けられているネットワーク アダプターに固有です。

返すことによって、OID 要求が完了する場合は、ミニポート ドライバーは、受信キューに、必要なソフトウェアとハードウェア リソースを割り当てることができますが正常に、 **NDIS\_状態\_成功**します。

ミニポート ドライバーでは、割り当てられた受信キューのキューの識別子を保持する必要があります。 NDIS は、受信キューに受信フィルターを設定、受信キューのパラメーターを変更または受信キューを解放するために、ミニポート ドライバーに後続の呼び出しを受信キューのキューの id を使用します。

それを発行する必要があります、上にあるドライバーを割り当ててまたはキューの受信し、必要に応じて、最初のフィルターを設定の詳細は、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](oid-receive-filter-queue-allocation-complete.md) OID 要求に割り当てが受信キューの現在のバッチの完了したミニポート ドライバーに通知を設定します。

フィルターがそのキューに設定されていない場合、ミニポート ドライバーは受信キュー内のすべてのパケットを保持する必要があります。 キューのなかった、フィルターを設定またはすべてのフィルターをクリアするには、キューを空にする必要があり、すべてのパケットを破棄する必要があります。 つまり、パケットはドライバー スタックを表示またはキューに保持できません。

上にあるドライバーを使用して、OID 要求[OID\_受信\_フィルター\_FREE\_キュー](oid-receive-filter-free-queue.md)を割り当て、キューを解放します。

### <a name="return-status-codes"></a>リターン状態コード

NDIS またはミニポート ドライバーのいずれかの OID の OID メソッド要求は、次のステータス コードのいずれかを返します\_受信\_フィルター\_ALLOCATE\_キュー。

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
<td><p>キューが正常に割り当てられます。 情報バッファーが含まれていますが、更新された<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_QUEUE_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)"> <strong>NDIS_RECEIVE_QUEUE_PARAMETERS</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>完了待ちになっています。 最終的な状態コードと結果は、呼び出し元の OID 要求完了ハンドラーに渡すことは。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>1 つ以上の上にあるドライバーが提供されているパラメーターが無効でした。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ</strong>.<strong>METHOD_INFORMATION</strong>.<strong>BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>ミニポート ドライバーの NDIS バージョン 6.20 が動作のバージョンよりも前です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_FAILURE</strong></p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
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
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

[**NET\_バッファー\_一覧\_受信\_キュー\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)

[OID\_受信\_フィルター\_FREE\_キュー](oid-receive-filter-free-queue.md)

[OID\_受信\_フィルター\_キュー\_割り当て\_完了](oid-receive-filter-queue-allocation-complete.md)

[**NDIS\_受信\_キュー\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

 

 




