---
title: OID_WWAN_USSD
description: OID_WWAN_USSD では、基になる MB デバイスに非構造化補助サービス データ (USSD) 要求を送信します。
ms.assetid: 9DFAAABD-8213-4B83-8FE8-1EC2BB9F735B
ms.date: 08/08/2017
keywords: -OID_WWAN_USSD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b22ec43ce164fe35053af42a9b4d3e7e3628458e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385489"
---
# <a name="oidwwanussd"></a>OID\_WWAN\_USSD


OID\_WWAN\_USSD MB の基になるデバイスに非構造化補助サービス データ (USSD) 要求を送信します。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[NDIS\_の状態\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd) USSD の最初の要求の状態を格納しているトランザクションが完了しているときに状態の通知。

Windows では、OID は送信しません\_WWAN\_USSD 要求ミニポート ドライバーを設定して保留中の操作を取り消す要求を除き、実行中の前回の要求がある場合に、 [WWAN\_USSD\_要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_ussd_request) **RequestType**メンバーへの要求の*WwanUssdRequestCancel*します。

要求が取り消されると、ミニポート ドライバーが取り消された要求とキャンセル要求の両方に応答する必要があります。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[NDIS\_状態\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)

[WWAN\_USSD\_要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_ussd_request)

 

 




