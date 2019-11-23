---
title: OID_WWAN_SMS_CONFIGURATION
description: OID_WWAN_SMS_CONFIGURATION によって、MB デバイスの SMS テキストメッセージ構成が設定または返されます。
ms.assetid: 3292a91d-4aa8-4c57-9223-d7d984dc5d69
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_SMS_CONFIGURATION
ms.localizationpriority: medium
ms.openlocfilehash: 95ad11e107489620a7037e5e23a8327b970c210b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843787"
---
# <a name="oid_wwan_sms_configuration"></a>OID\_WWAN\_SMS\_構成


OID\_WWAN\_SMS\_構成を設定するか、MB デバイスの SMS テキストメッセージ構成を返します。

ミニポートドライバーは、セット要求とクエリ要求を非同期的に処理し、最初に NDIS\_ステータス\_返して、元の要求に必要な\_を示します。その後、set 要求またはクエリ要求の完了に関係なく、 [ **\_の状態\_WWAN\_構成**](ndis-status-wwan-sms-configuration.md)状態通知を送信します。\_

クエリ要求では、デバイスまたはサブスクライバー Id モジュール (SIM) カードに格納されている、デバイスの現在の SMS テキストメッセージ構成が返されます。

Set 要求では、 [**NDIS\_WWAN\_設定\_sms\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration)構造を使用して、MB デバイスの sms テキストメッセージ構成を変更します。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN SMS の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)」を参照してください。

この OID を処理するとき、ミニポートドライバーは SIM カードにアクセスできますが、プロバイダーネットワークにアクセスすることはできません。

GSM ベースのデバイスのミニポートドライバーは、クエリと設定の両方の操作をサポートする必要があります。 CDMA ベースのデバイスのミニポートドライバーでは、クエリ操作のみをサポートする必要があります。 CDMA ベースのデバイスのミニポートドライバーは、クエリ要求のために、WWAN\_SMS\_構成構造の**Ulmaxmessageindex**メンバーで有効な値を返す必要があり、その他のメンバーは無視できます。

MB デバイスの SMS サブシステムが SMS 操作の準備ができている場合、ミニポートドライバーは、要求されていない NDIS\_ステータス\_WWAN\_SMS\_構成に送信する必要があります。 その後、OID\_WWAN\_SMS\_構成クエリ要求に応答する場合、ミニポートドライバーは、WWAN\_SMS\_構成構造のすべてのメンバーに対して有効な値を返す必要があります。

ミニポートドライバーは、デバイスが初期化されているが、SMS サブシステムがまだ初期化されていない場合は、NDIS\_STATUS\_\_を返す必要があります。

ミニポートドライバーでは、SMS テキストメッセージの構成がサポートされていない場合、NDIS\_の状態\_返され\_サポートされません。

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


[**NDIS\_WWAN\_\_SMS\_構成の設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration)

[**NDIS\_ステータス\_WWAN\_SMS\_構成**](ndis-status-wwan-sms-configuration.md)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




