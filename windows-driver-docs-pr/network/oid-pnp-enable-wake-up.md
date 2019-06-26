---
title: OID_PNP_ENABLE_WAKE_UP
description: OID_PNP_ENABLE_WAKE_UP
ms.assetid: 9afe774b-a429-413f-a7b6-3a3d79d2b95f
ms.date: 08/08/2017
keywords: -OID_PNP_ENABLE_WAKE_UP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6f027a8e49ad86fa06830da43de8f26e71ba6d55
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357669"
---
# <a name="oidpnpenablewakeup"></a>OID\_PNP\_を有効にする\_WAKE\_を





OID、セットとして\_PNP\_を有効にする\_WAKE\_OID をネットワーク アダプターのミニポート ドライバーを有効にする必要がありますウェイク アップ機能を指定します。

クエリ、OID として\_PNP\_を有効にする\_WAKE\_アップは、ネットワーク アダプターを有効になっている現在のウェイク アップ機能を取得します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、ビットマスクの組み合わせを有効にするために使用するフラグウェイク アップ イベント。

<a href="" id="ndis-pnp-wake-up-magic-packet"></a>**NDIS\_PNP\_WAKE\_を\_マジック\_パケット**  
設定すると、ミニポート ドライバーにマジック パケットの受信時にウェイク アップのイベントを通知するネットワーク アダプターが有効にする必要がありますを指定します。 (A*マジック パケット*は受信側のネットワーク アダプターのイーサネット アドレスの 16 個の連続したコピーを含むパケットです)。オフの場合、ミニポート ドライバーにこのようなウェイク アップ イベントをシグナル通知からのネットワーク アダプターが無効にする必要がありますを指定します。

<a href="" id="ndis-pnp-wake-up-pattern-match"></a>**NDIS\_PNP\_WAKE\_を\_パターン\_一致**  
設定すると、ミニポート ドライバーに、ネットワーク アダプターを使用して、プロトコルで指定されたパターンを含むパケットの受信時にウェイク アップ イベント通知が有効にする必要がありますを指定します[OID\_PNP\_追加\_ウェイク。\_\_パターン](oid-pnp-add-wake-up-pattern.md)します。 オフの場合、ミニポート ドライバーにこのようなウェイク アップ イベントをシグナル通知からのネットワーク アダプターが無効にする必要がありますを指定します。

<a href="" id="ndis-pnp-wake-up-link-change"></a>**NDIS\_PNP\_WAKE\_を\_リンク\_変更**  
予約済み。 NDIS は、このフラグは無視されます。

プロトコル ドライバーでのネットワーク アダプターのウェイク アップ機能を使用して[ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)関連付けられているネットワーク アダプターのウェイク アップ機能を有効にします。 プロトコル ドライバーには、ネットワーク アダプターにウェイク アップ機能が有効になっているかを判断するには、この OID クエリもできます。

NDIS はすぐにプロトコル ドライバーを指定するウェイク アップ機能を有効にします。 代わりに、NDIS プロトコル ドライバーに有効になっているウェイク アップ機能の追跡を維持し、ネットワーク アダプターは、低電力状態に遷移して、直前に NDIS 送信 OID\_PNP\_を有効にする\_WAKE\_セットを構成適切なウェイク アップ イベントを有効にするミニポート ドライバーに要求します。

ネットワーク アダプターの遷移を低電力状態にする前に (NDIS ミニポート ドライバーに送信する前に、 [OID\_PNP\_設定\_POWER](oid-pnp-set-power.md)要求)、NDIS OIDミニポートドライバーに送信\_PNP\_を有効にする\_WAKE\_アップ要求を適切なウェイク アップ機能を有効にします。

ミニポート ドライバーでは、有効または無効、ネットワーク アダプターにウェイク アップ イベントに適切なのデバイスに依存する手順を実行する必要があります。

NDIS は OID. 1.3 で設定するウェイク アップ機能をオフにする必要があります、ミニポート ドライバー\_PNP\_を有効にする\_WAKE\_をシステムが再開されます。 ウェイク アップ機能を再開の間で保持されませんする必要があります。 NDIS が、OID の設定を明示的にウェイク アップ機能を有効にすると場合、\_PNP\_を有効にする\_WAKE\_ミニポートの低電力状態に遷移する前にセットアップします。

上端がこの OID 要求を受信する中間のドライバーする必要があります、呼び出すことによって、基になるミニポート ドライバーに要求を常に反映されるまで、 [ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)または[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)関数。

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
<td><p>NDIS 6.0 および 6.1 ではサポートされています。 NDIS 6.20 が動作し、後で、使用して<a href="oid-pm-parameters.md" data-raw-source="[OID_PM_PARAMETERS](oid-pm-parameters.md)">OID_PM_PARAMETERS</a>代わりに)。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)

[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)

[OID\_PM\_パラメーター](oid-pm-parameters.md)

[OID\_PNP\_追加\_WAKE\_を\_パターン](oid-pnp-add-wake-up-pattern.md)

 

 




