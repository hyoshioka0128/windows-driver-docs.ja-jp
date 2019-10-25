---
title: OID_WWAN_SMS_DELETE
description: OID_WWAN_SMS_DELETE は、MB デバイス、サブスクライバー Id モジュール (SIM カード)、またはその他の補助非揮発性メモリまたはメモリに格納されている SMS テキストメッセージを削除します。
ms.assetid: b80fae94-35cc-4709-8346-d5a500d3fd49
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_SMS_DELETE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: ee57b0347db462fd9eb94f1faeda48d64bce9d68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843785"
---
# <a name="oid_wwan_sms_delete"></a>OID\_WWAN\_SMS\_削除


OID\_WWAN\_SMS\_DELETE は、MB デバイス、サブスクライバー Id モジュール (SIM カード)、またはその他の補助非揮発性メモリまたはメモリに格納されている SMS テキストメッセージを削除します。

クエリ要求はサポートされていません。

Set 要求では、 [**NDIS\_WWAN\_SMS\_削除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete)構造を使用します。

ミニポートドライバーは、この OID を非同期的に処理し、任意の set 要求に対して必要な一時的な応答\_通知\_NDIS\_の状態を返します。 ミニポートドライバーは、トランザクションが完了したときに[ **\_削除の通知\_\_、NDIS\_の状態**](ndis-status-wwan-sms-delete.md)を送信する必要があります。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN SMS の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)」を参照してください。

この OID を処理するとき、ミニポートドライバーはサブスクライバー Id モジュール (SIM カード) にアクセスできますが、プロバイダーのネットワークにはアクセスできません。

ミニポートドライバーは、インデックスに基づいて SMS テキストメッセージを削除したり、すべての SMS テキストメッセージを削除したりする要求を受信する場合があります。 Delete 要求は、新規 (未読) メッセージ、古い (読み取り) メッセージ、ドラフトメッセージ、送信メッセージなどの基本的なフィルターのいずれかで構成される場合があります。

ミニポートドライバーは、SMS テキストメッセージをサポートしていない場合、または SMS テキストメッセージを削除する機能がサポートされていない場合は、NDIS\_の状態\_\_返す必要があります。

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


[**NDIS\_WWAN\_SMS\_削除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




