---
title: OID_PNP_SET_POWER
description: OID_PNP_SET_POWER
ms.assetid: 21232db2-7484-4878-a2f9-5131c18ecf57
ms.date: 08/08/2017
keywords: -OID_PNP_SET_POWER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6e687ccde70836eb28837730b26c7064ddfee7c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382893"
---
# <a name="oidpnpsetpower"></a>OID\_PNP\_設定\_電源





OID\_PNP\_設定\_POWER OID がその基になるネットワーク アダプターで指定されたデバイスの電源状態に遷移がミニポート ドライバーに通知、 *InformationBuffer*します。 デバイスの電源の状態は、次のいずれかとして指定[ **NDIS\_デバイス\_POWER\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_device_power_state)値。

-   **NdisDeviceStateD0**
-   **NdisDeviceStateD1**
-   **NdisDeviceStateD2**
-   **NdisDeviceStateD3**

OID\_PNP\_設定\_POWER 要求は続く可能性があります、 [OID\_PNP\_クエリ\_POWER](oid-pnp-query-power.md)要求。

NDIS 6.30 以降、NDIS いない一時停止し、次の条件に該当する場合は、電源状態遷移中にドライバー スタックで NDIS ドライバーを再起動します。

-   基になるミニポート ドライバー セット、 **NDIS\_ミニポート\_属性\_いいえ\_一時停止\_ON\_SUSPEND**フラグ、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造体。 ドライバーがその呼び出しでこの構造体へのポインターを渡します、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数。

-   NDIS 6.30 または以降のバージョンの NDIS ミニポート ドライバーに関連付けられているすべての上にあるフィルター ドライバーをサポートします。

-   NDIS 6.30 または以降のバージョンの NDIS ミニポート ドライバーにバインドされているすべての上にあるプロトコル ドライバーをサポートします。

### <a name="transitioning-to-a-low-power-state-d1-d3"></a>低電力状態 (D1 D3) への移行

ミニポート ドライバーが OID のセット要求を処理するときに\_PNP\_設定\_低電力状態に遷移する電源、次を実行する必要があります。

-   完全に指定されたネットワーク デバイスの電源状態のネットワーク アダプターを準備します。 これを実現するミニポート ドライバーによって実行されるタスクは、デバイスによって異なります。

-   呼び出しの待機、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を返します。

-   ネットワーク アダプターによって処理された送信要求を完了するまで待ちます。 完了すると、ミニポート ドライバーを呼び出す必要があります、 [ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数。 ドライバーを設定する必要があります、**状態**の各メンバー [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体を適切な NDIS\_状態\_ *Xxx*値。

-   すべての保留中の送信要求を呼び出すことによって完了、 [ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数。 ドライバーを設定する必要があります、**状態**の各メンバー [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体を**NDIS\_ステータス\_低\_POWER\_状態**します。

-   すべての新しい送信要求を拒否、 [ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)関数を呼び出すことによってすぐに、 [ **NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数。 ドライバーを設定する必要があります、**状態**の各メンバー [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体を**NDIS\_ステータス\_低\_POWER\_状態**します。

NDIS 6.30 と以降のバージョンの NDIS をサポートしているミニポート ドライバーは、次の方法もする必要があります。

-   保留中の完了の呼び出しを通じてインジケーターを受信するを待ちませんその[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)関数。 また、ミニポート ドライバーを変更する必要がありますいない、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体または完了を待機しているすべてのパケットのデータ。

-   OID の処理\_PNP\_設定\_電源要求の一時停止または実行中のいずれかのアダプター状態から低電力状態にします。 これらの状態の詳細については、次を参照してください。[ミニポート アダプターの状態と操作](https://docs.microsoft.com/windows-hardware/drivers/network/miniport-adapter-states-and-operations)します。

D3 の状態に遷移する場合、ネットワーク アダプター、前に、次のタスクを実行することによって、ミニポート ドライバーが、ミニポート ドライバーの管理下にあるすべてをオフにする必要があります。

-   割り込みと DMA エンジン、ネットワーク アダプターを無効にします。

-   ネットワーク アダプターの受信エンジンを停止します。

-   割り当てを解除または修正されません記述子を受信し、保留中に関連付けられているパケット バッファー受信表示します。

-   すべての NDIS タイマーをキャンセルします。

**注**  ミニポート ドライバーは、バス ドライバーに D3 の状態にネットワーク アダプターが遷移した後に、ネットワーク アダプターにアクセスできません。

 

### <a name="transitioning-to-the-full-power-state-d0"></a>電力の状態 (D0) への移行

ミニポート ドライバーが OID のセット要求を処理するときに\_PNP\_設定\_電力状態に遷移する電源受信エンジンの前の状態にネットワーク アダプターの受信エンジンに復元する必要が、アダプターは、低電力状態に移行されました。

**注**  ミニポート ドライバーのアクセスまたは任意の受信を変更する必要がありますされません保留中に関連付けられているバッファーがインジケーターを受信します。

 

NDIS ミニポート ドライバーの呼び出す[ *MiniportRestart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)関数の後、完全な電源への移行状態 NDIS がドライバーと呼ばれるかどうかのみ[ *MiniportPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)低電力状態に遷移する前に関数。

**注**  中間のドライバーが常に返す必要があります**NDIS\_状態\_成功**OID のクエリに\_PNP\_設定\_電源。 中間のドライバーは、OID を伝達することはありません\_PNP\_設定\_電源要求の基になる、ミニポート ドライバーにします。

 

## <a name="return-status-codes"></a>リターン状態コード


ミニポート ドライバーの[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数は、次のいずれかがこの要求の値を返します。

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
<td><p>ミニポート ドライバーでは、要求が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)"> <strong>NdisMOidRequestComplete</strong> </a> NDIS_STATUS_SUCCESS を渡して、関数、<em>状態</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>ミニポート ドライバーがリセットされています。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 5.1、および NDIS 6.0 以降がサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)

[*MiniportPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)

[*MiniportRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)

[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)

[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)

[**NDIS\_デバイス\_POWER\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_device_power_state)

[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)

[**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

 

 




