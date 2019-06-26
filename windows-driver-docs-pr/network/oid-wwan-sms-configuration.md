---
title: OID_WWAN_SMS_CONFIGURATION
description: OID_WWAN_SMS_CONFIGURATION を設定または MB デバイスの SMS テキスト メッセージの構成を取得します。
ms.assetid: 3292a91d-4aa8-4c57-9223-d7d984dc5d69
ms.date: 08/08/2017
keywords: -OID_WWAN_SMS_CONFIGURATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f285c21c3b0bc8010de3beb3493e13ddb44eeae9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361172"
---
# <a name="oidwwansmsconfiguration"></a>OID\_WWAN\_SMS\_構成


OID\_WWAN\_SMS\_構成が MB デバイスの SMS テキスト メッセージの構成を取得または設定します。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_SMS\_構成**](ndis-status-wwan-sms-configuration.md)セットまたはクエリの要求の完了に関係なく、状態の通知。

クエリ要求には、MB デバイスの現在 SMS テキスト メッセージの構成、デバイスまたはサブスクライバー Identity モジュール (SIM) カードに格納されているが返されます。

セットの使用を要求する、 [ **NDIS\_WWAN\_設定\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration) MB デバイスの SMS テキスト メッセージの構成を変更する構造体.

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)します。

この OID を処理するときに、ミニポート ドライバーは、SIM カードにアクセスできますが、プロバイダーのネットワークにアクセスしないでください。

GSM ベースのデバイスのミニポート ドライバーは、両方のクエリをサポートし、操作を設定する必要があります。 CDMA ベースのデバイスのミニポート ドライバーでは、クエリ操作のみをサポートする必要があります。 CDMA ベースのデバイスのミニポート ドライバーが有効な値を返す必要があります、 **ulMaxMessageIndex** 、WWAN のメンバー\_SMS\_構成は、クエリ要求用の構造し、その他のメンバーを無視することができます。

ミニポート ドライバーが要請されていない NDIS を送信する必要があります\_状態\_WWAN\_SMS\_SMS 操作の準備ができたら、MB デバイスの SMS サブシステムの構成を示す値。 その後、OID に応答するとき\_WWAN\_SMS\_構成のクエリを要求するミニポート ドライバーが、WWAN のすべてのメンバーの有効な値を返す必要があります\_SMS\_構成構造体。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_デバイスが初期化されましたが、SMS サブシステムはまだ初期化されていない場合、初期化します。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_SMS テキスト メッセージの構成をサポートしていない場合にサポートされています。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_設定\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration)

[**NDIS\_状態\_WWAN\_SMS\_構成**](ndis-status-wwan-sms-configuration.md)

[WWAN SMS の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




