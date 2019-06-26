---
title: NDIS_STATUS_WWAN_PREFERRED_PROVIDERS
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 通知を使用して、優先プロバイダー一覧 (PPL) に変更された MB サービスに通知します。
ms.assetid: b0c06db9-82ca-4f94-80e6-3cf13197abf5
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_PREFERRED_PROVIDERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 115c02b4338ee27334dafe5fb6ea7d18b63500a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377615"
---
# <a name="ndisstatuswwanpreferredproviders"></a>NDIS\_状態\_WWAN\_優先\_プロバイダー


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_優先\_MB サービス優先プロバイダー一覧 (PPL) が変更されたことを通知するためにプロバイダーの通知。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_優先\_プロバイダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)構造体。

<a name="remarks"></a>注釈
-------

場合によっては、PPL (GSM ベースのデバイス) はネットワークによって更新されますか Over-The-Air (OTA) やショート メッセージ サービス (SMS) でします。 ミニポート ドライバーでは、PPL を適宜更新する必要があります。 その後、ミニポート ドライバーはこのを示す値を使用して、更新された PPL での更新に関する MB サービスに通知する必要があります。 GSM ベースのネットワークの場合、 **PreferredListHeader** NDIS のメンバー\_WWAN\_優先\_プロバイダーの構造は、更新された PPL を指す必要があります。

ミニポート ドライバーでは、このを示す値を使用して、結果として更新プログラムに関する MB サービスに通知する、 [OID\_WWAN\_優先\_プロバイダー](oid-wwan-preferred-providers.md) MB サービスからの要求のセット。 OID への応答を\_WWAN\_優先\_プロバイダー セット要求内の 0 個の要素を含める必要があります、 **PreferredListHeader**メンバー。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)

[OID\_WWAN\_優先\_プロバイダー](oid-wwan-preferred-providers.md)

 

 




