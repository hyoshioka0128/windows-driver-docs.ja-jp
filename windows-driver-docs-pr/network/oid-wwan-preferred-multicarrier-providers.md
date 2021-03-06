---
title: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS を使用して、優先する複数の通信事業者ネットワーク プロバイダーの一覧を照会または設定します。 マルチ キャリア プロバイダーは、ホーム プロバイダーとして設定できるものです。
ms.assetid: BA78E0B9-1B57-412C-83E7-328F8304C82D
ms.date: 08/08/2017
keywords: -OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 753dd6da2f49bc748e8d8f21949a162f32918746
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360762"
---
# <a name="oidwwanpreferredmulticarrierproviders"></a>OID\_WWAN\_優先\_マルチ\_プロバイダー


OID\_WWAN\_優先\_マルチ\_プロバイダーを使用する*設定*または*クエリ*優先の複数の通信事業者ネットワーク プロバイダーの一覧。 マルチ キャリア プロバイダーは、可能性のあるもの*設定*ホーム プロバイダーとしてサポートします。

両方*設定*と*クエリ*要求がサポートされています。 ミニポート ドライバーを処理する必要があります*設定*と*クエリ*NDIS を返す非同期的に、最初に要求\_状態\_INDICATION\_元に必要な要求、およびそれ以降の送信、 [ **NDIS\_状態\_WWAN\_優先\_マルチ\_プロバイダー** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)状態通知を含む、 [ **NDIS\_WWAN\_優先\_マルチ\_プロバイダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)構造体。

ミニポート ドライバーを設定する必要があります、 **PreferredListHeader.ElementType**メンバー **WwanStructProvider2**と**PreferredListHeader.ElementCount**メンバーをOID に応答するときに、リスト内のプロバイダーの番号\_WWAN\_優先\_プロバイダー*クエリ*要求。 返されるマルチ キャリア プロバイダー、*クエリ*優先マルチ キャリア一覧は、サービスに返される時に、ホーム プロバイダーとして設定できる必要があります。

ミニポート ドライバーを設定する必要があります、 **PreferredListHeader.ElementType**メンバー **WwanStructProvider2**と**PreferredListHeader.ElementCount**場合は 0 をメンバーOID に応答して\_WWAN\_優先\_プロバイダー*設定*要求。

エラー ミニポートを設定する必要があります、 **uStatus**の NDIS メンバー\_WWAN\_優先\_マルチ\_障害状態プロバイダーの構造と**PreferredListHeader.ElementCount**を 0 にし、 **PreferredLIstHeader.ElementType**に**WwanStructProvider2**します。

**Rssi**と**ErrorRate** WWAN のメンバー\_PROVIDER2 構造は、使用可能な場合、設定する必要があります。

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
<td><p>バージョン:Windows 8 および Windows の以降のバージョンでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_優先\_マルチ\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

[**NDIS\_状態\_WWAN\_優先\_マルチ\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)

[MB プロバイダー操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




