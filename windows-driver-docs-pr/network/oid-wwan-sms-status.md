---
title: OID_WWAN_SMS_STATUS
description: OID_WWAN_SMS_STATUS MB デバイスのメッセージ ストアの状態を報告します。
ms.assetid: a43451e6-f589-4963-acc7-855555655d37
ms.date: 08/08/2017
keywords: -OID_WWAN_SMS_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 91c1e0fcaa8d32bb5f484d05b57d09e83846b997
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384719"
---
# <a name="oidwwansmsstatus"></a>OID\_WWAN\_SMS\_状態


OID\_WWAN\_SMS\_状態 MB デバイスのメッセージ ストアの状態を報告します。

要求のセットがサポートされていません。

クエリ要求では、構造体は使用しないでください。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_SMS\_状態**](ndis-status-wwan-sms-status.md)クエリ要求を完了するときは、MB デバイスのメッセージ ストアの状態を示す状態通知します。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)します。

この OID を処理するときに、ミニポート ドライバーは Subscriber Identity Module (SIM カード) にアクセスできますが、プロバイダーのネットワークにアクセスしないでください。

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


[WWAN SMS の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

[**NDIS\_状態\_WWAN\_SMS\_状態**](ndis-status-wwan-sms-status.md)

 

 




