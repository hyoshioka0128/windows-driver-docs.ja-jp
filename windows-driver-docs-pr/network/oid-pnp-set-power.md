---
title: OID_PNP_SET_POWER
description: OID_PNP_SET_POWER
ms.assetid: 21232db2-7484-4878-a2f9-5131c18ecf57
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_PNP_SET_POWER
ms.localizationpriority: medium
ms.openlocfilehash: 67bfd40a8c88918d5fe2c29a84b657dfc03f8ee0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844035"
---
# <a name="oid_pnp_set_power"></a>OID\_PNP\_設定\_電源





OID\_PNP\_SET\_POWER OID は、基になるネットワークアダプターが*Informationbuffer*に指定されたデバイスの電源状態に移行することをミニポートドライバーに通知します。 デバイスの電源状態は、次のいずれかの[**NDIS\_デバイス\_電源\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)の値として指定されます。

-   **NdisDeviceStateD0**
-   **NdisDeviceStateD1**
-   **NdisDeviceStateD2**
-   **NdisDeviceStateD3**

POWER request\_設定されている OID\_PNP\_の前に、 [\_PNP\_クエリ\_の電源](oid-pnp-query-power.md)要求があることがあります。

Ndis 6.30 以降、次の条件に該当する場合、NDIS は電源状態の移行中にドライバースタック内の NDIS ドライバーを一時停止して再起動しません。

-   基になるミニポートドライバーは、ndis [ **\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造の\_**SUSPEND フラグに\_一時停止\_\_、NDIS\_ミニポート\_属性**を設定します。 ドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数の呼び出しで、この構造体へのポインターを渡します。

-   ミニポートドライバーに関連付けられているすべてのフィルタードライバーは、NDIS 6.30 以降のバージョンの NDIS をサポートしています。

-   ミニポートドライバーにバインドされているすべてのプロトコルドライバーは、ndis 6.30 以降のバージョンの NDIS をサポートしています。

### <a name="transitioning-to-a-low-power-state-d1-d3"></a>低電力状態への移行 (D1-D3)

ミニポートドライバーが OID\_\_設定要求を処理するときに、電源\_電力を低電力状態に移行するように設定した場合は、次の操作を行う必要があります。

-   ネットワークデバイスの電源状態を示すネットワークアダプターを完全に準備します。 これを実現するためにミニポートドライバーによって実行されるタスクは、デバイスに依存します。

-   [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数への呼び出しが返されるまで待機します。

-   ネットワークアダプターによって処理された送信要求が完了するまで待機します。 完了すると、ミニポートドライバーは[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出す必要があります。 ドライバーは、各[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**status**メンバーを、適切な NDIS\_status\_*Xxx*値に設定する必要があります。

-   [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出して、保留中のすべての送信要求を完了します。 ドライバーは、各[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**Status**メンバーを**NDIS\_status\_低\_電力\_状態**に設定する必要があります。

-   [**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数を呼び出して、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数に対して行われたすべての新しい送信要求を直ちに拒否します。 ドライバーは、各[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**Status**メンバーを**NDIS\_status\_低\_電力\_状態**に設定する必要があります。

Ndis 6.30 以降のバージョンの NDIS をサポートするミニポートドライバーでは、次の操作も行う必要があります。

-   [*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)関数の呼び出しによって、保留中の受信通知が完了するまで待機しません。 また、ミニポートドライバーは、完了を待機しているすべてのパケットについて、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体またはデータを変更することはできません。

-   OID\_PNP を処理し、一時停止または実行中のアダプターの状態から電力要求\_電力の状態を低電力状態に設定\_ます。 これらの状態の詳細については、「[ミニポートアダプターの状態と操作](https://docs.microsoft.com/windows-hardware/drivers/network/miniport-adapter-states-and-operations)」を参照してください。

ネットワークアダプターが D3 状態に移行する前に、ミニポートドライバーは、次のタスクを実行して、ミニポートドライバーの制御下にあるすべてをオフにする必要があります。

-   ネットワークアダプターの割り込みと DMA エンジンを無効にします。

-   ネットワークアダプターの受信エンジンを停止します。

-   受信記述子と、保留中の受信通知に関連付けられているパケットバッファーは、割り当てを解除したり変更したりしないでください。

-   すべての NDIS タイマーをキャンセルします。

バスドライバーがネットワークアダプターを D3 状態に移行した後に、ミニポートドライバーがネットワークアダプターにアクセスできない  に**注意**してください。

 

### <a name="transitioning-to-the-full-power-state-d0"></a>フルパワー状態への移行 (D0)

ミニポートドライバーが OID\_\_PNP の set 要求を処理するときに、電源\_電力状態に移行するように設定されている場合は、アダプターが低電力状態に遷移する前に、ネットワークアダプターの受信エンジンを受信エンジンと同じ状態に復元する必要があります。

ミニポートドライバーは、保留中の受信確認に関連付けられているすべての受信バッファーにアクセスしたり、変更したりすることはできない  に**注意**してください。

 

Ndis は、低電力状態に移行する前に、NDIS がドライバーの[*Miniportrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)関数を呼び出した場合にのみ、ミニポートドライバーの[*miniportrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出します。

中間ドライバーは、 **\_の状態\_正常**に実行する必要があり**ます  、** OID\_PNP\_設定\_電力。 中間のドライバーは、\_電源要求を、基になるミニポートドライバーに設定することによって、OID\_の PNP\_伝達しないようにする必要があります。

 

## <a name="return-status-codes"></a>ステータスコードを返す


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
<td><p>ミニポートドライバーは、要求を非同期的に完了します。 ミニポートドライバーはすべての処理を完了した後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>関数を呼び出し、 <em>STATUS</em>パラメーターに NDIS_STATUS_SUCCESS を渡すことによって、要求を成功させる必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポートドライバーがリセットされています。</p></td>
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
<td><p>NDIS 5.1、および NDIS 6.0 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[*MiniportPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)

[*MiniportRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)

[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)

[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)

[**NDIS\_デバイス\_電源\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)

[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

 

 




