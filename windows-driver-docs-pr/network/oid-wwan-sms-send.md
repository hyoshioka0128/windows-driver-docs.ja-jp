---
title: OID_WWAN_SMS_SEND
description: OID_WWAN_SMS_SEND は、SMS テキストメッセージを別の MB デバイスに送信します。
ms.assetid: 557d2bdc-8414-4fcb-903c-23bb68955d07
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_SMS_SEND ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 6e06857ffcba24dcc15ca621990a95ba95427d7e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843782"
---
# <a name="oid_wwan_sms_send"></a>OID\_WWAN\_SMS\_送信


OID\_WWAN\_SMS\_では、SMS テキストメッセージを別の MB デバイスに送信します。

クエリ要求はサポートされていません。

Set 要求では、 [**NDIS\_WWAN\_SMS\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)構造を使用します。

ミニポートドライバーは、この OID を非同期的に処理し、任意の set 要求に対して必要な一時的な応答\_通知\_NDIS\_の状態を返します。 ミニポートドライバーは、クライアントがトランザクションを完了したときに通知を[**送信する\_、\_\_の NDIS\_状態**](ndis-status-wwan-sms-send.md)を送信する必要があります。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN SMS の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)」を参照してください。

この OID を処理するとき、ミニポートドライバーはプロバイダーネットワークにアクセスできますが、サブスクライバー Id モジュール (SIM カード) にはアクセスできません。

OID\_WWAN\_SMS\_SEND は、デバイスの機能に応じて、PDU モードと CDMA モードの両方の SMS テキストメッセージの送信をサポートします。

GSM ベースのデバイスは、PDU モードの SMS テキストメッセージのみをサポートすることが想定されています。 CDMA ベースのデバイスは、CDMA モードの SMS テキストメッセージのみをサポートすることが想定されています。 ミニポートドライバーは、SMS テキストメッセージモードに関係なく、設定された要求を完了できる必要があります。

ミニポートドライバーは、SMS テキストメッセージをサポートしていない場合、または SMS テキストメッセージを送信する機能がサポートされていない場合は、NDIS\_の状態\_\_返す必要があります。

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


[**NDIS\_WWAN\_SMS\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




