---
title: OID_WWAN_SMS_SEND
description: OID_WWAN_SMS_SEND MB の別のデバイスに SMS テキスト メッセージを送信します。
ms.assetid: 557d2bdc-8414-4fcb-903c-23bb68955d07
ms.date: 08/08/2017
keywords: -OID_WWAN_SMS_SEND ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 895b2e76ae38ea12b3fe9a5ecb2d6bf72fcefc79
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383185"
---
# <a name="oidwwansmssend"></a>OID\_WWAN\_SMS\_送信


OID\_WWAN\_SMS\_送信 MB の別のデバイスに SMS テキスト メッセージを送信します。

クエリ要求はサポートされていません。

セットの使用を要求する、 [ **NDIS\_WWAN\_SMS\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)構造体。

ミニポート ドライバーは、この OID を非同期に処理し、NDIS を返す必要があります\_状態\_INDICATION\_セットの要求に必要な作業 provisional 応答。 ミニポート ドライバーに送信する必要があります、 [ **NDIS\_状態\_WWAN\_SMS\_送信**](ndis-status-wwan-sms-send.md)トランザクションが完了しているときを示す値。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)します。

この OID を処理するときに、ミニポート ドライバーは、プロバイダーのネットワークにアクセスできますが、Subscriber Identity Module (SIM カード) にアクセスしないでください。

OID\_WWAN\_SMS\_送信は、デバイスの機能によって、PDU モードと CDMA モード SMS テキスト メッセージの送信をサポートしています。

PDU モード SMS テキスト メッセージのみをサポートするためには、GSM ベースのデバイスが必要です。 CDMA モード SMS テキスト メッセージのみをサポートするためには、CDMA ベースのデバイスが必要です。 ミニポート ドライバーでは、SMS テキスト メッセージ モードに関係なくセット要求を完了できる必要があります。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_SMS テキスト メッセージ、または SMS テキスト メッセージを送信する機能をサポートしていない場合にサポートされます。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_SMS\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)

[WWAN SMS の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




