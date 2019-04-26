---
title: OID_PNP_SET_POWER
description: OID_PNP_SET_POWER
ms.assetid: 21232db2-7484-4878-a2f9-5131c18ecf57
ms.date: 08/08/2017
keywords: -OID_PNP_SET_POWER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 902d2fd60d315c3430194c7e19f835178b11f330
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342974"
---
# <a name="oidpnpsetpower"></a>OID\_PNP\_設定\_電源





OID\_PNP\_設定\_POWER OID がその基になるネットワーク アダプターで指定されたデバイスの電源状態に遷移がミニポート ドライバーに通知、 *InformationBuffer*します。 デバイスの電源の状態は、次のいずれかとして指定[ **NDIS\_デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/gg602135)値。

-   **NdisDeviceStateD0**
-   **NdisDeviceStateD1**
-   **NdisDeviceStateD2**
-   **NdisDeviceStateD3**

OID\_PNP\_設定\_POWER 要求は続く可能性があります、 [OID\_PNP\_クエリ\_POWER](oid-pnp-query-power.md)要求。

NDIS 6.30 以降、NDIS いない一時停止し、次の条件に該当する場合は、電源状態遷移中にドライバー スタックで NDIS ドライバーを再起動します。

-   基になるミニポート ドライバー セット、 **NDIS\_ミニポート\_属性\_いいえ\_一時停止\_ON\_SUSPEND**フラグ、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 ドライバーがその呼び出しでこの構造体へのポインターを渡します、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

-   NDIS 6.30 または以降のバージョンの NDIS ミニポート ドライバーに関連付けられているすべての上にあるフィルター ドライバーをサポートします。

-   NDIS 6.30 または以降のバージョンの NDIS ミニポート ドライバーにバインドされているすべての上にあるプロトコル ドライバーをサポートします。

### <a name="transitioning-to-a-low-power-state-d1-d3"></a>低電力状態 (D1 D3) への移行

ミニポート ドライバーが OID のセット要求を処理するときに\_PNP\_設定\_低電力状態に遷移する電源、次を実行する必要があります。

-   完全に指定されたネットワーク デバイスの電源状態のネットワーク アダプターを準備します。 これを実現するミニポート ドライバーによって実行されるタスクは、デバイスによって異なります。

-   呼び出しの待機、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数を返します。

-   ネットワーク アダプターによって処理された送信要求を完了するまで待ちます。 完了すると、ミニポート ドライバーを呼び出す必要があります、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)関数。 ドライバーを設定する必要があります、**状態**の各メンバー [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体を適切な NDIS\_状態\_ *Xxx*値。

-   すべての保留中の送信要求を呼び出すことによって完了、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)関数。 ドライバーを設定する必要があります、**状態**の各メンバー [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体を**NDIS\_ステータス\_低\_POWER\_状態**します。

-   すべての新しい送信要求を拒否、 [ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)関数を呼び出すことによってすぐに、 [ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)関数。 ドライバーを設定する必要があります、**状態**の各メンバー [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体を**NDIS\_ステータス\_低\_POWER\_状態**します。

NDIS 6.30 と以降のバージョンの NDIS をサポートしているミニポート ドライバーは、次の方法もする必要があります。

-   保留中の完了の呼び出しを通じてインジケーターを受信するを待ちませんその[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)関数。 また、ミニポート ドライバーを変更する必要がありますいない、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体または完了を待機しているすべてのパケットのデータ。

-   OID の処理\_PNP\_設定\_電源要求の一時停止または実行中のいずれかのアダプター状態から低電力状態にします。 これらの状態の詳細については、次を参照してください。[ミニポート アダプターの状態と操作](https://msdn.microsoft.com/library/windows/hardware/ff560490)します。

D3 の状態に遷移する場合、ネットワーク アダプター、前に、次のタスクを実行することによって、ミニポート ドライバーが、ミニポート ドライバーの管理下にあるすべてをオフにする必要があります。

-   割り込みと DMA エンジン、ネットワーク アダプターを無効にします。

-   ネットワーク アダプターの受信エンジンを停止します。

-   割り当てを解除または修正されません記述子を受信し、保留中に関連付けられているパケット バッファー受信表示します。

-   すべての NDIS タイマーをキャンセルします。

**注**  ミニポート ドライバーは、バス ドライバーに D3 の状態にネットワーク アダプターが遷移した後に、ネットワーク アダプターにアクセスできません。

 

### <a name="transitioning-to-the-full-power-state-d0"></a>電力の状態 (D0) への移行

ミニポート ドライバーが OID のセット要求を処理するときに\_PNP\_設定\_電力状態に遷移する電源受信エンジンの前の状態にネットワーク アダプターの受信エンジンに復元する必要が、アダプターは、低電力状態に移行されました。

**注**  ミニポート ドライバーのアクセスまたは任意の受信を変更する必要がありますされません保留中に関連付けられているバッファーがインジケーターを受信します。

 

NDIS ミニポート ドライバーの呼び出す[ *MiniportRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff559435)関数の後、完全な電源への移行状態 NDIS がドライバーと呼ばれるかどうかのみ[ *MiniportPause*](https://msdn.microsoft.com/library/windows/hardware/ff559418)低電力状態に遷移する前に関数。

**注**  中間のドライバーが常に返す必要があります**NDIS\_状態\_成功**OID のクエリに\_PNP\_設定\_電源。 中間のドライバーは、OID を伝達することはありません\_PNP\_設定\_電源要求の基になる、ミニポート ドライバーにします。

 

## <a name="return-status-codes"></a>リターン状態コード


ミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数は、次のいずれかがこの要求の値を返します。

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
<td><p>ミニポート ドライバーでは、要求を非同期的に実行されます。 ミニポート ドライバーには、すべての処理が完了したら後、は、呼び出すことによって、要求が成功する必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a> NDIS_STATUS_SUCCESS を渡して、関数、<em>状態</em>パラメーター。</p></td>
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
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[*MiniportPause*](https://msdn.microsoft.com/library/windows/hardware/ff559418)

[*MiniportRestart*](https://msdn.microsoft.com/library/windows/hardware/ff559435)

[*MiniportReturnNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559437)

[*MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440)

[**NDIS\_デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/gg602135)

[**NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)

[**NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)

[**NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

 

 




