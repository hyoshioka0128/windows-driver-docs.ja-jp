---
title: OID_WWAN_SMS_SEND
description: OID_WWAN_SMS_SEND MB の別のデバイスに SMS テキスト メッセージを送信します。
ms.assetid: 557d2bdc-8414-4fcb-903c-23bb68955d07
ms.date: 08/08/2017
keywords: -OID_WWAN_SMS_SEND ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dfc0f9196d3aab2b6254f70e3ae435eeca1d145f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571383"
---
# <a name="oidwwansmssend"></a>OID\_WWAN\_SMS\_送信


OID\_WWAN\_SMS\_送信 MB の別のデバイスに SMS テキスト メッセージを送信します。

クエリ要求はサポートされていません。

セットの使用を要求する、 [ **NDIS\_WWAN\_SMS\_送信**](https://msdn.microsoft.com/library/windows/hardware/ff567943)構造体。

ミニポート ドライバーは、この OID を非同期に処理し、NDIS を返す必要があります\_状態\_INDICATION\_セットの要求に必要な作業 provisional 応答。 ミニポート ドライバーに送信する必要があります、 [ **NDIS\_状態\_WWAN\_SMS\_送信**](ndis-status-wwan-sms-send.md)トランザクションが完了しているときを示す値。

<a name="remarks"></a>コメント
-------

詳細については、この OID を使用して、[WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)を参照してください。

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


[**NDIS\_WWAN\_SMS\_送信**](https://msdn.microsoft.com/library/windows/hardware/ff567943)

[WWAN SMS の操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)

 

 




