---
title: OID_WWAN_SMS_DELETE
description: OID_WWAN_SMS_DELETE MB デバイス、または Subscriber Identity Module (SIM カード)、またはその他の補助非揮発性メモリまたはメモリに格納されている SMS テキスト メッセージを削除します。
ms.assetid: b80fae94-35cc-4709-8346-d5a500d3fd49
ms.date: 08/08/2017
keywords: -OID_WWAN_SMS_DELETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6d2d971f74bc8996fe7f02e41204eae9f94f26ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527958"
---
# <a name="oidwwansmsdelete"></a>OID\_WWAN\_SMS\_削除


OID\_WWAN\_SMS\_MB デバイス、または Subscriber Identity Module (SIM カード)、またはその他の補助非揮発性メモリまたはメモリに格納されている SMS テキスト メッセージを削除します。

クエリ要求はサポートされていません。

セットの使用を要求する、 [ **NDIS\_WWAN\_SMS\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff567938)構造体。

ミニポート ドライバーは、この OID を非同期に処理し、NDIS を返す必要があります\_状態\_INDICATION\_セットの要求に必要な作業 provisional 応答。 ミニポート ドライバーに送信する必要があります、 [ **NDIS\_状態\_WWAN\_SMS\_削除**](ndis-status-wwan-sms-delete.md)トランザクションが完了しているときを示す値。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、次を参照してください。 [WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)します。

この OID を処理するときに、ミニポート ドライバーは Subscriber Identity Module (SIM カード) にアクセスできますが、プロバイダーのネットワークにアクセスしないでください。

ミニポート ドライバー、インデックスに基づく SMS テキスト メッセージを削除するか、すべての SMS テキスト メッセージを削除する要求が表示されます。 削除要求は、(未読) の新しいメッセージ、メッセージの古い (読み取り)、ドラフトのメッセージまたは送信されたメッセージなどの基本的なフィルターのいずれかで構成されます。

ミニポート ドライバーは、NDIS を返す必要があります\_状態\_いない\_SMS テキスト メッセージ、または SMS テキスト メッセージを削除する機能をサポートしていない場合にサポートされます。

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


[**NDIS\_WWAN\_SMS\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff567938)

[WWAN SMS の操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)

 

 




