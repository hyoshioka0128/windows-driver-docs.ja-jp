---
title: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS は、優先するマルチキャリアネットワークプロバイダーの一覧を設定または照会するために使用されます。 マルチキャリアプロバイダーは、ホームプロバイダーとして設定できるものです。
ms.assetid: BA78E0B9-1B57-412C-83E7-328F8304C82D
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
ms.localizationpriority: medium
ms.openlocfilehash: 43f87b7a2173dabb20661ed5aea1aa5599b577b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843811"
---
# <a name="oid_wwan_preferred_multicarrier_providers"></a>OID\_WWAN\_優先\_マルチキャリア\_プロバイダー


OID\_\_優先\_マルチキャリア\_プロバイダーは、優先するマルチキャリアネットワークプロバイダーの一覧を*設定*または*照会*するために使用されます。 マルチキャリアプロバイダーは、ホームプロバイダーとして*設定*できるものです。

*セット*要求と*クエリ*要求の両方がサポートされています。 ミニポートドライバーは、*セット*および*クエリ*要求を非同期的に処理し、最初に ndis\_状態\_を返してから、元の要求に必要な\_を示します。その後、ndis\_[**WWAN\_\_マルチキャリア\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)構造を含む\_\_の\_[**マルチキャリア\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)状態通知を送信します。\_

ミニポートドライバーでは、 **PreferredListHeader**メンバーを**WwanStructProvider2**に設定し、 **PREFERREDLISTHEADER**のメンバーを、OID\_WWAN\_優先\_プロバイダーの*クエリ*要求に応答するときにリスト内のプロバイダーの数に設定する必要があります。 *クエリ*で返されるマルチキャリアプロバイダーは、優先されるマルチキャリアリストがサービスに返されるときにホームプロバイダーとして設定できる必要があります。

ミニポートドライバーでは、 **PreferredListHeader**メンバーを**WwanStructProvider2**に設定し、PreferredListHeader にを設定する必要があります。は、OID\_\_\_WWAN に応答するときに、に設定する必要があります。

エラーミニポートでは、NDIS\_WWAN\_優先\_マルチキャリア\_PROVIDERS 構造体の**uStatus**メンバーを、エラー状態と**PreferredListHeader**に0、 **PreferredListHeader**を**WwanStructProvider2**に設定する必要があります。

WWAN\_PROVIDER2 構造体の**Rssi**および**errorrate**メンバーは、使用可能な場合は設定する必要があります。

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
<td><p>バージョン: Windows 8 以降のバージョンの Windows でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_優先\_マルチキャリア\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

[**NDIS\_ステータス\_WWAN\_優先\_マルチキャリア\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)

[MB プロバイダーの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




