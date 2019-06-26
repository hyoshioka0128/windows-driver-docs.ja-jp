---
title: OID_RECEIVE_FILTER_QUEUE_PARAMETERS
description: 上にあるドライバーは、オブジェクト識別子 OID_RECEIVE_FILTER_QUEUE_PARAMETERS の受信キューの現在の構成パラメーターを取得する (OID) のメソッドを要求を発行します。
ms.assetid: f6cd7896-0811-4029-b1d8-8cf800d7813e
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_QUEUE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d6b76956a9a159f14834695654672507cd208aab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376764"
---
# <a name="oidreceivefilterqueueparameters"></a>OID\_受信\_フィルター\_キュー\_パラメーター


上にあるドライバーは、オブジェクト識別子の OID (OID) メソッドの要求を発行\_受信\_フィルター\_キュー\_受信キューの現在の構成パラメーターを取得するパラメーター。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)の種類のキュー id を使用した構造**NDIS\_受信\_キュー\_ID**します。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造体にはへのポインターが含まれています、 **NDIS\_受信\_キュー\_パラメーター**構造体。

OID の要求を設定しました OID ドライバーの問題を重なって\_受信\_フィルター\_キュー\_キューの現在の構成パラメーターを変更するパラメーター。 上にあるドライバーへのポインターを提供する、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体。

<a name="remarks"></a>注釈
-------

OID の要求を設定しました OID ドライバーの問題を重なって\_受信\_フィルター\_キュー\_受信キューの 1 つ以上のパラメーターを変更するパラメーター。 OID のセット要求は、NDIS 6.20 が動作し、それ以降のミニポート ドライバーでは省略可能です。 ただし、OID 要求は、仮想マシン キュー (VMQ) インターフェイスをサポートするミニポート ドライバーに対して必須です。

**注**  OID が OID の要求を設定してキューを割り当て、上にあるドライバーが発行することによって構成パラメーターを変更できるだけ\_受信\_フィルター\_キュー\_パラメーター.

 

上にあるドライバーは、以前からキューの識別子の入力値を取得[OID\_受信\_フィルター\_ALLOCATE\_キュー](oid-receive-filter-allocate-queue.md)メソッド要求の OID。

対応するフラグを変更する構成パラメーターを変更できる上にあるドライバーが、キューを割り当てた後 (NDIS\_受信\_キュー\_パラメーター\_*Xxx*\_CHANGED) で、**フラグ**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体。 ただし、キューが割り当てられた後、上にあるドライバーは、構成パラメーターがない、対応するフラグを変更を変更できません。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID メソッド要求を処理する NDIS\_受信\_フィルター\_キュー\_ミニポート ドライバー、および次のステータス コードを返します。 1 つのパラメーター。

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
<td><p>完了待ちになっています。 NDIS では、要求が完了した後、最終的な状態コードと結果を呼び出し元の OID 要求完了ハンドラーに渡すは。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ</strong>.<strong>METHOD_INFORMATION</strong>.<strong>BytesNeeded</strong> NDIS_OID_REQUEST 構造体に必要な最小バッファー サイズを内のメンバー。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_PARAMETER</strong></p></td>
<td><p>基になるネットワーク アダプターがサポートされていない機能を有効にしようとした要求が失敗しました。</p></td>
</tr>
<tr class="odd">
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

[**NDIS\_受信\_キュー\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[OID\_受信\_フィルター\_ALLOCATE\_キュー](oid-receive-filter-allocate-queue.md)

[OID\_受信\_フィルター\_キュー\_パラメーター](oid-receive-filter-queue-parameters.md)

 

 




