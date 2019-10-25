---
title: NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 通知を使用して、前の OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERSquery 要求に応答します。また、この通知を使用して、MB サービスからの OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS set 要求の結果として、MB サービスに更新に関する情報を通知することもできます。 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS set 要求への応答には、PreferredListHeader メンバーにゼロ要素が含まれている必要があります。 また、ミニポートドライバーは、この通知を使用して要請されていないイベントを送信して、推奨されるマルチキャリアプロバイダーリスト (PMCPL) が変更されたことを MB サービスに通知することもできます。この通知では、NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 構造体が使用されます。
ms.assetid: DBE8911D-1A92-40BC-94EB-BED3B8B82CB0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: d5ec5345a77efbcc88edd9d7d82e988e9f69dc71
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844699"
---
# <a name="ndis_status_wwan_preferred_multicarrier_providers"></a>NDIS\_ステータス\_WWAN\_優先\_マルチキャリア\_プロバイダー


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_優先\_マルチキャリア\_プロバイダーの通知を使用して、以前の OID\_WWAN に応答し、[マルチキャリア\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-multicarrier-providers)*クエリ*要求。

また、ミニポートドライバーは、この通知を使用して、mb サービスからの要求をマルチキャリア\_PROVIDERS\_優先\_プロバイダーが*設定*した\_結果として、更新プログラムに関する情報を mb サービスに通知することもできます。 OID\_WWAN\_推奨される\_マルチキャリア\_プロバイダーの*設定*要求に対する応答には、 **PreferredListHeader**メンバー内に0個の要素が含まれている必要があります。 また、ミニポートドライバーは、この通知を使用して要請されていないイベントを送信して、推奨されるマルチキャリアプロバイダーリスト (PMCPL) が変更されたことを MB サービスに通知することもできます。

この通知では、 [**NDIS\_WWAN\_優先\_マルチキャリア\_PROVIDERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)構造体を使用します。

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
<td><p>Windows 8 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_優先\_マルチキャリア\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

 

 




