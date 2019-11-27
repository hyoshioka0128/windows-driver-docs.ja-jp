---
title: OID_PNP_ENABLE_WAKE_UP
description: OID_PNP_ENABLE_WAKE_UP
ms.assetid: 9afe774b-a429-413f-a7b6-3a3d79d2b95f
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_PNP_ENABLE_WAKE_UP
ms.localizationpriority: medium
ms.openlocfilehash: 6d9b3de8297e6b9c001a7014356d3819119841a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844039"
---
# <a name="oid_pnp_enable_wake_up"></a>\_\_ウェイクアップ\_を有効にする OID\_の PNP





設定として、\_ウェイク\_UP OID を有効にする OID\_PNP\_は、ミニポートドライバーがネットワークアダプターで有効にするウェイクアップ機能を指定します。

クエリとして、OID\_PNP\_有効にすると\_WAKE\_UP は、ネットワークアダプターに対して有効になっている現在のウェイクアップ機能を取得します。

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーは、ウェイクアップイベントの組み合わせを有効にするために使用できるフラグのビットマスクです。

<a href="" id="ndis-pnp-wake-up-magic-packet"></a>**NDIS\_PNP\_ウェイクアップ\_\_マジック\_パケット**  
設定されている場合、ミニポートドライバーが、マジックパケットの受信時にウェイクアップイベントを通知するように、ネットワークアダプターを有効にする必要があることを指定します。 (*マジックパケット*は、受信側のネットワークアダプターのイーサネットアドレスの連続した16個のコピーを含むパケットです)。オフにすると、ミニポートドライバーがネットワークアダプターによるウェイクアップイベントの通知を無効にするように指定します。

<a href="" id="ndis-pnp-wake-up-pattern-match"></a>**NDIS\_PNP\_ウェイクアップ\_\_パターン\_一致**  
設定すると、ポートで指定されたパターンを含むパケットを受信したときに、ミニポートドライバーによって、ネットワークアダプターがウェイクアップイベントに信号を送ることを許可するように指定します。これにより、 [\_wake\_up\_パターン\_追加して、\_プロトコルによって指定されたパターンが含まれます。](oid-pnp-add-wake-up-pattern.md). オフにすると、ミニポートドライバーがネットワークアダプターによるウェイクアップイベントの通知を無効にするように指定します。

<a href="" id="ndis-pnp-wake-up-link-change"></a>**NDIS\_PNP\_ウェイクアップ\_アップ\_リンク\_変更**  
予約済み。 NDIS は、このフラグを無視します。

プロトコルドライバーは、NDIS のネットワークアダプターのウェイクアップ機能を使用して[ **\_パラメーターを\_バインド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)し、関連付けられているネットワークアダプターのウェイクアップ機能を有効にします。 また、プロトコルドライバーはこの OID に対してクエリを実行し、ネットワークアダプターに対して有効になっているウェイクアップ機能を特定することもできます。

NDIS では、プロトコルドライバーで指定されているウェイクアップ機能をすぐに有効にすることはできません。 代わりに、NDIS は、プロトコルドライバーが有効になっているウェイクアップ機能を追跡します。また、ネットワークアダプターが低電力状態に移行する直前に、NDIS によって、\_WAKE\_UP set 要求をミニポートに\_有効にするための OID\_PNP が送信されます。ドライバーを使用して、適切なウェイクアップイベントを有効にします。

ネットワークアダプターが低電力状態に移行する前 (つまり、NDIS が、電源要求\_設定された[oid\_pnp\_](oid-pnp-set-power.md) ) を送信する前に、ndis はミニポートドライバーに対して、\_pnp\_有効にし\_WAKE を有効にします。適切なウェイクアップ機能を有効にするための要求を\_します。

ミニポートドライバーは、ネットワークアダプターでウェイクアップイベントを有効または無効にするために、デバイスに依存する適切な手順を実行する必要があります。

ミニポートドライバーは、NDIS によって設定されたウェイクアップ機能をクリアし、システムが再開されたときに\_ウェイクアップ\_を有効に\_\_ます。 ウェイクアップ機能は、再開時に保持しないでください。 ウェイクアップ機能が有効になっている場合、NDIS は、ポートが低電力状態に移行する前に\_ウェイクアップ\_を有効にするように、OID\_\_PNP に明示的に設定します。

上端がこの OID 要求を受け取る中間ドライバーは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)または[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)関数を呼び出すことによって、常に要求を基になるミニポートドライバーに伝達する必要があります。

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
<td><p>NDIS 6.0 および6.1 でサポートされています。 NDIS 6.20 以降の場合は、代わりに<a href="oid-pm-parameters.md" data-raw-source="[OID_PM_PARAMETERS](oid-pm-parameters.md)">OID_PM_PARAMETERS</a>を使用します)。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)

[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)

[OID\_PM\_パラメーター](oid-pm-parameters.md)

[OID\_PNP\_追加\_ウェイクアップ\_上\_パターン](oid-pnp-add-wake-up-pattern.md)

 

 




