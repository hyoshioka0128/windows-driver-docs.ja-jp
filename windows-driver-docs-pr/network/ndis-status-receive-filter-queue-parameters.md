---
title: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS
description: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS 状態は、NDIS と仮想マシン (VM) キューの現在のパラメーターは、ネットワーク アダプター上で変更されたドライバーの上にあることを示します。
ms.assetid: 30782C77-578F-4533-8B6B-9D2F64EE6189
ms.date: 08/08/2017
keywords: -NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0a3422c806c07e27ad07a9ea58951abfb0c81749
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385241"
---
# <a name="ndisstatusreceivefilterqueueparameters"></a>NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター


**NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター** NDIS と関連付けたドライバーに状態を示しますが、現在の仮想マシン (VM) のキューネットワーク アダプターのパラメーターが変更されました。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター** VM キューの現在のパラメーターがある場合、状態の表示ネットワーク アダプターに変更します。 次の条件のいずれかが true の場合、VM のキューのパラメーターを変更できます。

-   VM のキューのパラメーターは、独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションで変更されます。

-   負荷分散マルチプレクサー中間ドライバーによって管理されているフェールオーバー (LBFO) のチームに属している 1 つまたは複数のネットワーク アダプターの VM キューのパラメーターを変更します。 詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)します。

ミニポート ドライバーを発行したとき、 **NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター**状態を示す値、次の手順に従う必要があります。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)ネットワーク アダプターでは、現在の VM キュー パラメーターを含む構造体。 ドライバーを設定する必要がありますも、**フラグ**適切な NDIS を使用して、この構造体のメンバー\_受信\_キュー\_パラメーター\_*Xxx* \_変更されたフラグをレポートする**NDIS\_受信\_キュー\_パラメーター**が変更されたメンバーの値。

    **注**NDIS 6.30 以降、ミニポート ドライバーのみを発行でき、 **NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター**状態レポートを示す値を変更する、 **InterruptCoalescingDomainId**メンバー。




ミニポート ドライバーを初期化すると、**ヘッダー**この構造体のメンバーは、設定、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。 ミニポート ドライバーのセット、**リビジョン**のメンバー**ヘッダー** NDIS に\_受信\_キュー\_パラメーター\_リビジョン\_2 と**サイズ**NDIS メンバー\_SIZEOF\_受信\_キュー\_パラメーター\_リビジョン\_2。


2.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)次のように構造体。

    -   **StatusCode**にメンバーを設定する必要があります**NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター**します。

    -   **StatusBuffer**へのポインターにメンバーを設定する必要があります、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体。 この構造体には、NIC のスイッチの現在有効になっているハードウェア機能が含まれています。

    -   **StatusBufferSize** sizeof にメンバーを設定する必要があります ([**NDIS\_受信\_キュー\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters))。

3.  ミニポート ドライバーが呼び出すことによって、状態の通知を発行[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体を*StatusIndication*パラメーター。

使用できるドライバーが重なって、 **NDIS\_状態\_受信\_フィルター\_キュー\_パラメーター**でキュー パラメーターの状態を示す値を現在の VM を確認ネットワーク アダプター。 また、これらのドライバーも発行できますオブジェクト識別子 (OID) のクエリ要求の[OID\_受信\_フィルター\_キュー\_パラメーター](oid-receive-filter-queue-parameters.md)をいつでもこれらのパラメーターを取得します。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_受信\_キュー\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_受信\_フィルター\_キュー\_パラメーター](oid-receive-filter-queue-parameters.md)








