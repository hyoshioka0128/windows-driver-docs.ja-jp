---
title: NDIS_STATUS_WWAN_PREFERRED_PROVIDERS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 通知を使用して、優先プロバイダーリスト (PPL) が変更されたことを MB サービスに通知します。
ms.assetid: b0c06db9-82ca-4f94-80e6-3cf13197abf5
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_PREFERRED_PROVIDERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ef3a982061a1ddd75c3aca9d7d669c3bd091e766
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844698"
---
# <a name="ndis_status_wwan_preferred_providers"></a>NDIS\_ステータス\_WWAN\_優先\_プロバイダー


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_優先\_プロバイダーの通知を使用して、優先プロバイダーリスト (PPL) が変更されたことを MB サービスに通知します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)の構造を使用します。

<a name="remarks"></a>注釈
-------

場合によっては、PPL (GSM ベースのデバイスの場合) は、無線 (OTA) またはショートメッセージサービス (SMS) のいずれかでネットワークによって更新されます。 ミニポートドライバーは、それに応じて PPL を更新する必要があります。 その後、ミニポートドライバーは、更新された PPL でこの表示を使用して、更新プログラムに関する情報を MB サービスに通知する必要があります。 GSM ベースのネットワークの場合、NDIS\_WWAN\_優先\_プロバイダーの構造の**PreferredListHeader**メンバーは、更新された PPL を指す必要があります。

ミニポートドライバーは、この表示を使用して、mb サービスからの要求 設定された[\_プロバイダーの OID\_\_](oid-wwan-preferred-providers.md)の結果として、更新プログラムに関する情報を mb サービスに通知します。 OID\_WWAN\_推奨される\_プロバイダーの設定要求に対する応答には、 **PreferredListHeader**メンバー内にゼロ要素が含まれている必要があります。

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
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)

[OID\_WWAN\_優先\_プロバイダー](oid-wwan-preferred-providers.md)

 

 




