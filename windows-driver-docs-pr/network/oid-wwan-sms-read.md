---
title: OID_WWAN_SMS_READ
description: OID_WWAN_SMS_READ MB デバイス、または Subscriber Identity Module (SIM カード)、またはその他の補助非揮発性メモリまたはメモリに格納されている SMS テキスト メッセージを読み取ります。
ms.assetid: f4dbb7e8-1348-4fa8-abac-f644a443df48
ms.date: 08/08/2017
keywords: -OID_WWAN_SMS_READ ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 36c3efe3fadfc6a15ac79b3506e16bbf7d1e7b85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361158"
---
# <a name="oidwwansmsread"></a>OID\_WWAN\_SMS\_読み取り


OID\_WWAN\_SMS\_読み取り MB のデバイスまたは Subscriber Identity Module (SIM カード)、またはその他の補助非揮発性メモリまたはメモリに格納されている SMS テキスト メッセージを読み取ります。

要求のセットがサポートされていません。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_SMS\_受信**](ndis-status-wwan-sms-receive.md)状態通知を含む、 [ **NDIS\_WWAN\_SMS\_読み取る**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read)クエリ要求を完了するときに、呼び出し元が最初に指定した SMS メッセージの要求を提供する構造体。

SMS テキスト メッセージの読み取りを要求する呼び出し元の提供、NDIS\_WWAN\_SMS\_SMS メッセージ、呼び出し元を返すミニポートを示す読み取り構造体。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)します。

この OID を処理するときに、ミニポート ドライバーは Subscriber Identity Module (SIM カード) にアクセスできますが、プロバイダーのネットワークにアクセスしないでください。

OID\_WWAN\_SMS\_読み取りは、デバイスの機能によって、PDU モードと CDMA モード SMS テキスト メッセージの読み取りをサポートしています。

ミニポート ドライバー、インデックスに基づく SMS テキスト メッセージを読み取る、またはすべての SMS テキスト メッセージの読み取り要求が表示されます。 読み取り要求は可能性があります (未読) の新しいメッセージ、メッセージの古い (読み取り)、ドラフトのメッセージまたは送信されたメッセージなどの基本的なフィルターのいずれかで構成されます。

SMS テキスト メッセージ機能を実装するミニポート ドライバーは、の基本的なフィルターを使用して、新しいメッセージの読み取りをサポートする必要があります*WwanSmsFlagNew*します。 その他のすべてのフィルターの種類では、サポートするために省略可能です。

ミニポート ドライバーは、物理的に別の使用可能なすべての SMS テキスト メッセージ ストア間で 1 つの SMS テキスト メッセージ ストアをプロジェクトに論理的にする必要があります。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_SMS テキスト メッセージをサポートしていない場合にサポートされています。

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


[**NDIS\_WWAN\_SMS\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read)

[WWAN SMS の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




