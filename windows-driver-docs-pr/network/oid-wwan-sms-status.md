---
title: OID_WWAN_SMS_STATUS
description: OID_WWAN_SMS_STATUS MB デバイスのメッセージ ストアの状態を報告します。
ms.assetid: a43451e6-f589-4963-acc7-855555655d37
ms.date: 08/08/2017
keywords: -OID_WWAN_SMS_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 151e4bc2b0a2b6414c31a9ec1b0a5276b3c65623
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560144"
---
# <a name="oidwwansmsstatus"></a>OID\_WWAN\_SMS\_状態


OID\_WWAN\_SMS\_状態 MB デバイスのメッセージ ストアの状態を報告します。

要求のセットがサポートされていません。

クエリ要求では、構造体は使用しないでください。

ミニポート ドライバーは、最初に、非同期的には、NDIS を返すクエリ要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[ **NDIS\_状態\_WWAN\_SMS\_状態**](ndis-status-wwan-sms-status.md)クエリ要求を完了するときは、MB デバイスのメッセージ ストアの状態を示す状態通知します。

<a name="remarks"></a>注釈
-------

詳細については、この OID を使用して、[WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)を参照してください。

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


[WWAN SMS の操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)

[**NDIS\_状態\_WWAN\_SMS\_状態**](ndis-status-wwan-sms-status.md)

 

 




