---
title: OID_WWAN_SMS_READ
description: OID_WWAN_SMS_READ は、MB デバイス、サブスクライバー Id モジュール (SIM カード)、またはその他の補助非揮発性メモリまたはメモリに格納されている SMS テキストメッセージを読み取ります。
ms.assetid: f4dbb7e8-1348-4fa8-abac-f644a443df48
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_SMS_READ ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a3b8fd7c35443f3dc1db96f0753ab5d453bcfe99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843783"
---
# <a name="oid_wwan_sms_read"></a>OID\_WWAN\_SMS\_読み取り


OID\_WWAN\_SMS\_読み取りは、MB デバイスに格納されている SMS テキストメッセージ、またはサブスクライバー Id モジュール (SIM カード)、またはその他の補助非揮発性メモリまたはメモリに格納されているメッセージを読み取ります。

Set 要求はサポートされていません。

ミニポートドライバーでは、クエリ要求を非同期的に処理し、最初に NDIS\_の\_状態を返し、元の要求に必要な\_を示し、その後、 [**ndis\_ステータス\_WWAN\_SMS\_を送信する必要があり**](ndis-status-wwan-sms-receive.md)要求の完了時に呼び出し元によって最初に提供された sms メッセージを提供するために、 [**NDIS\_WWAN\_SMS\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read)構造を含むステータス通知を受信します。

SMS テキストメッセージの読み取りを要求している呼び出し元は、NDIS\_WWAN\_SMS\_読み取り構造を提供し、呼び出し元がどの SMS メッセージを返して返すかを示すことができます。

<a name="remarks"></a>注釈
-------

この OID の使用方法の詳細については、「 [WWAN SMS の操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)」を参照してください。

この OID を処理する場合、ミニポートドライバーはサブスクライバー Id モジュール (SIM カード) にアクセスできますが、プロバイダーネットワークにアクセスすることはできません。

OID\_WWAN\_SMS\_READ は、デバイスの機能に応じて、PDU モードと CDMA モードの両方の SMS テキストメッセージの読み取りをサポートします。

ミニポートドライバーは、インデックスに基づいて SMS テキストメッセージを読み取るか、すべての SMS テキストメッセージを読み取る要求を受け取ることができます。 読み取り要求は、新規 (未読) メッセージ、古い (読み取り) メッセージ、ドラフトメッセージ、送信メッセージなどの基本的なフィルターのいずれかで構成される場合があります。

SMS テキストメッセージ機能を実装するミニポートドライバーは、 *Wwansmsflagnew*の基本的なフィルターを使用して、新しいメッセージの読み取りをサポートする必要があります。 その他のフィルターの種類はすべてオプションでサポートされます。

ミニポートドライバーは、すべての使用可能な物理的に異なる SMS テキストメッセージストアにわたって、1つの SMS テキストメッセージストアを論理的に射影する必要があります。

ミニポートドライバーは、SMS テキストメッセージをサポートしていない場合、サポートされてい\_ないため、NDIS\_の状態\_返される必要があります。

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


[**NDIS\_WWAN\_SMS\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_read)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




