---
title: OID_WWAN_USSD
description: OID_WWAN_USSD は、非構造化補助サービスデータ (USSD) 要求を基になる MB のデバイスに送信します。
ms.assetid: 9DFAAABD-8213-4B83-8FE8-1EC2BB9F735B
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_WWAN_USSD ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 822ebc8f8ea000704c2a5ba85634cd494b32e93e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843765"
---
# <a name="oid_wwan_ussd"></a>OID\_WWAN\_USSD


OID\_WWAN\_USSD は、非構造化補助サービスデータ (USSD) 要求を基になる MB のデバイスに送信します。

クエリ要求はサポートされていません。

ミニポートドライバーは、set 要求を非同期に処理し、最初に NDIS\_状態\_返して、元の要求に必要な\_を示します。その後、 [ndis\_ステータス\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd) status に送信します。トランザクションが完了したときの初期の USSD 要求の状態を含む通知。

以前の要求がまだ進行中である場合、Windows は、\_[USSD\_要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_request)**を設定することによって保留中の操作をキャンセルする要求を除き、\_USSD 要求をミニポートドライバーに\_送信しません。** *Wwanussdrequestcancel*に対する要求の RequestType メンバー。

要求が取り消されると、ミニポートドライバーは、取り消された要求とキャンセル要求の両方に応答する必要があります。

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
<td><p>Windows 8 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[NDIS\_ステータス\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)

[WWAN\_USSD\_要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_request)

 

 




