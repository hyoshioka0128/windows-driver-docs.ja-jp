---
title: OID_WWAN_VISIBLE_PROVIDERS
description: OID_WWAN_VISIBLE_PROVIDERS は、現在 MB のデバイスの範囲内に表示されているネットワークプロバイダーの一覧を返します。
ms.assetid: 4dfd4477-6332-4163-8b3e-a1604b11d175
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_VISIBLE_PROVIDERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: b061f28de86d13b47b7c5c8d74d63f467de36507
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843763"
---
# <a name="oid_wwan_visible_providers"></a>OID\_WWAN\_表示される\_プロバイダー


OID\_WWAN\_表示される\_プロバイダーは、現在 MB のデバイス範囲内に表示されているネットワークプロバイダーの一覧を返します。

Set 要求はサポートされていません。

ミニポートドライバーでは、クエリ要求を非同期的に処理し、最初に NDIS\_STATUS を返し、元の要求に対して必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_表示されるように\_する必要があり\_プロバイダー**](ndis-status-wwan-visible-providers.md) [ **\_WWAN\_含まれる**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)プロバイダーの状態通知は、クエリ要求の完了時に表示されるネットワークプロバイダーに関する情報を提供するために、表示される\_プロバイダーの構造を示します。

*クエリ*要求では、NDIS\_WWAN\_入力として表示\_プロバイダーの構造\_取得します。 WWAN\_GET\_VISIBLE の**アクション**メンバーが表示されている場合\_プロバイダーは、表示されている\_プロバイダーを取得\_、すべてのミニポートから表示可能なすべてのプロバイダーが返されます。 WWAN\_GET\_VISIBLE の**アクション**メンバーが表示されている場合\_プロバイダーは、表示されている\_プロバイダー\_を取得します。\_プロバイダーを取得します。この場合、ミニポートは、表示可能なマルチキャリアプロバイダーを返す必要があります。ホームプロバイダーとして設定します。

デバイスによって返される表示プロバイダーの一覧では、プロバイダーごとにプロバイダーの状態が正しく設定されている必要があります。 たとえば、マルチキャリア優先プロバイダーは、WWAN\_プロバイダーの\_状態\_優先\_マルチキャリアとしてタグ付けされている必要があります。また、現在のホームプロバイダーについては、どのような\_タグを使用する必要があるかを指定します。HOME、現在登録されているプロバイダーについては、\_プロバイダー\_状態\_登録済みであることを示すタグを付ける必要があります。

WWAN\_PROVIDER2 構造体の**Rssi**および**errorrate**メンバーは、使用可能な場合は設定する必要があります。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN プロバイダーの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)」を参照してください。

ミニポートドライバーは、クエリ操作を処理するときにサブスクライバー Id モジュール (SIM カード) にアクセスできますが、プロバイダーネットワークにはアクセスできません。

ミニポートドライバーは、 **VisibleListHeader**メンバーを*WwanStructProvider*に設定する必要があります。

CDMA ベースのネットワークの場合、優先ローミングリスト (PRL) 内のいずれかのネットワークが現在表示されている場合、ミニポートドライバーはホームプロバイダーのみを返します。 GSM ベースのネットワークでは、表示されているプロバイダーの一覧に複数のプロバイダーが存在する場合があります。

接続中に表示されているプロバイダーのスキャンをサポートしていないデバイスは、NDIS\_\_\_WWAN の**uStatus**メンバーにある WWAN\_STATUS\_BUSY エラー値を返す必要があります。

GSM ベースのデバイスと CDMA ベースのデバイスは両方とも、登録モードで表示されているプロバイダーのスキャンをサポートする必要があります。 ただし、パケットデータプロトコル (PDP) コンテキストがアクティブな場合 (デバイスがプロバイダーのネットワークに接続されている場合など)、表示されているプロバイダーのスキャンをサポートするためにミニポートドライバーは必要ありません。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_表示される\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)

[**NDIS\_ステータス\_WWAN\_表示されている\_プロバイダ**](ndis-status-wwan-visible-providers.md)

[WWAN プロバイダーの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




