---
title: OID_WWAN_PREFERRED_PROVIDERS
description: OID_WWAN_PREFERRED_PROVIDERS は、GSM ベースのデバイスの優先プロバイダーの一覧に関する情報を返します。
ms.assetid: fa70f1ac-5b14-44f8-a2c4-d2163fe81c5a
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_PREFERRED_PROVIDERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 4bafac81046a5e112ef8f7814d645b8d1f99de4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843810"
---
# <a name="oid_wwan_preferred_providers"></a>OID\_WWAN\_優先\_プロバイダー


OID\_WWAN\_優先\_プロバイダーは、GSM ベースのデバイスの優先プロバイダーの一覧に関する情報を返します。 CDMA ベースのデバイスのミニポートドライバーでは、この OID をサポートする必要はありません。

ミニポートドライバーは、セットおよびクエリ要求を非同期的に処理し、最初に NDIS\_\_STATUS を返し、元の要求に対して必要な\_を通知してから、後で[**ndis\_ステータス\_WWAN\_を送信する必要があります。** ](ndis-status-wwan-preferred-providers.md) [**NDIS\_WWAN\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)の構造を含む\_プロバイダーの状態通知。設定またはクエリ要求の完了に関係なく、優先プロバイダーリスト (PPL) に関する情報を提供します。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN プロバイダーの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)」を参照してください。

ミニポートドライバーは、クエリ要求を処理するときにサブスクライバー Id モジュール (SIM カード) にアクセスできますが、プロバイダーネットワークにはアクセスできません。

ミニポートドライバーは、set 要求を処理するときに、サブスクライバー Id モジュール (SIM カード) またはプロバイダーネットワークにアクセスできます。

OID\_WWAN\_優先\_プロバイダーを処理する場合、ミニポートドライバーでは、WWAN\_プロバイダーの\_状態\_優先または WWAN\_プロバイダー\_状態\_禁止フラグを設定することができます。entries. 非対応プロバイダーは、GSM ベースのデバイスの一覧に表示されない場合があることに注意してください。

ミニポート driverrs は、 **PreferredListHeader**メンバーを*WwanStructProvider*に設定する必要があります。 OID\_WWAN に応答する場合は、ミニポートドライバーで**PreferredListHeader**メンバーを0に設定する必要があります。これは、優先\_プロバイダーによって設定される要求\_ます。

セット要求を処理するときに、デバイスの PPL を上書きできるかどうかは、デバイスの機能、携帯電話テクノロジ、およびネットワークプロバイダーのポリシーによって異なります。

ミニポートドライバーは、NDIS\_ステータス\_返す必要がありますが、PPL の戻りまたは設定がサポートされていない場合はサポートされませ\_ん。

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


[**NDIS\_WWAN\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)

[**NDIS\_ステータス\_WWAN\_優先\_プロバイダー**](ndis-status-wwan-preferred-providers.md)

[WWAN プロバイダーの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




