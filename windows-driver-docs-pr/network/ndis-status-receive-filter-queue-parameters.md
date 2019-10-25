---
title: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS
description: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS の状態は、ネットワークアダプターで現在の仮想マシン (VM) キューのパラメーターが変更されたことを、NDIS およびそれ以降のドライバーに示します。
ms.assetid: 30782C77-578F-4533-8B6B-9D2F64EE6189
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d8fda407edcca4ff5814de5cabc0891694784505
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843522"
---
# <a name="ndis_status_receive_filter_queue_parameters"></a>NDIS\_ステータス\_受信\_フィルター\_キューの\_パラメーター


**Ndis\_ステータス\_受信\_フィルター\_キュー\_パラメーター**の状態は、ネットワークアダプターで現在の仮想マシン (VM) キューのパラメーターが変更されたことを ndis およびそれ以降のドライバーに示します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、ネットワークアダプターで現在の VM キューパラメーターが変更されている場合に **\_フィルター\_キュー\_パラメーターを受信\_\_、NDIS の状態**を発行する必要があります。 VM キューのパラメーターは、次のいずれかの条件に該当する場合に変更される可能性があります。

-   VM キューのパラメーターは、独立系ハードウェアベンダー (IHV) によって開発された管理アプリケーションを使用して変更されます。

-   VM キューパラメーターは、MUX 中間ドライバーによって管理される負荷分散フェールオーバー (LBFO) チームに属する1つまたは複数のネットワークアダプターに対して変更されます。 詳細については、「 [NDIS MUX 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)」を参照してください。

ミニポートドライバーが NDIS\_の状態を発行し **\_\_フィルター\_キューの\_パラメーター**の状態が表示されたら、次の手順に従う必要があります。

1.  ミニポートドライバーは、ネットワークアダプターの現在の VM キューパラメーターを使用して、 [ **\_キュー\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)初期化します。 また、ドライバーは、この構造体の**フラグ**メンバーを適切な NDIS\_RECEIVE\_queue に設定する必要があります。\_*Xxx*\_変更されたフラグを、 **ndis\_receive\_queue のレポートに\_し @no__t**変更されたパラメーターのメンバー値 (_s)。

    **メモ** NDIS 6.30 以降では、ミニポートドライバーは、 **InterruptCoalescingDomainId**メンバーへの変更についてレポートするための **\_キュー\_パラメーターの状態を受信\_\_、NDIS\_の状態**のみを発行できます。




ミニポートドライバーは、この構造体の**ヘッダー**メンバーを初期化するときに、**ヘッダー**の**TYPE**メンバーを NDIS\_OBJECT\_type\_DEFAULT に設定します。 ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_RECEIVE\_QUEUE\_パラメーター\_リビジョン\_2 および**SIZE**メンバーを NDIS\_SIZEOF\_receive\_queue に設定します。\_パラメーター\_REVISION\_2 です。


2.  ミニポートドライバーは、次の方法で[**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体を初期化します。

    -   **StatusCode**メンバーを**NDIS\_STATUS に設定し\_受信\_フィルター\_キュー\_パラメーター**に設定する必要があります。

    -   **Statusbuffer**メンバーは、 [**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体へのポインターに設定する必要があります。 この構造体には、NIC スイッチの現在有効なハードウェア機能が含まれています。

    -   **Statusbuffersize**メンバーを Sizeof ([**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)) に設定する必要があります。

3.  ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出すことによって状態通知を発行します。 ドライバーは、 [**NDIS\_STATUS\_を示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)ポインターを*statusindication*パラメーターに渡す必要があります。

これまでのドライバーでは、 **NDIS の\_ステータス\_受信\_フィルター\_キュー\_パラメーター**の状態の表示を使用して、ネットワークアダプターの現在の VM キューパラメーターを確認できます。 また、これらのドライバーは Oid のオブジェクト識別子 (OID) クエリ要求を発行して、これらのパラメーターをいつでも取得[\_フィルター\_キュー\_パラメーター\_受け取る](oid-receive-filter-queue-parameters.md)こともできます。

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
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_\_フィルター\_\_キューのパラメーターを受け取る](oid-receive-filter-queue-parameters.md)








