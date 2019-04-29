---
title: OID_WWAN_USSD
description: OID_WWAN_USSD では、基になる MB デバイスに非構造化補助サービス データ (USSD) 要求を送信します。
ms.assetid: 9DFAAABD-8213-4B83-8FE8-1EC2BB9F735B
ms.date: 08/08/2017
keywords: -OID_WWAN_USSD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7ac8ac570b99b641aa3b3833fc1a528eeae97a5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383181"
---
# <a name="oidwwanussd"></a>OID\_WWAN\_USSD


OID\_WWAN\_USSD MB の基になるデバイスに非構造化補助サービス データ (USSD) 要求を送信します。

クエリ要求はサポートされていません。

ミニポート ドライバーが非同期的に、最初に返す NDIS セット要求を処理する必要があります\_状態\_INDICATION\_元の要求とそれ以降の送信に必要な[NDIS\_の状態\_WWAN\_USSD](https://msdn.microsoft.com/library/windows/hardware/hh439822) USSD の最初の要求の状態を格納しているトランザクションが完了しているときに状態の通知。

Windows では、OID は送信しません\_WWAN\_USSD 要求ミニポート ドライバーを設定して保留中の操作を取り消す要求を除き、実行中の前回の要求がある場合に、 [WWAN\_USSD\_要求](https://msdn.microsoft.com/library/windows/hardware/hh464138) **RequestType**メンバーへの要求の*WwanUssdRequestCancel*します。

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


[NDIS\_状態\_WWAN\_USSD](https://msdn.microsoft.com/library/windows/hardware/hh439822)

[WWAN\_USSD\_要求](https://msdn.microsoft.com/library/windows/hardware/hh464138)

 

 




