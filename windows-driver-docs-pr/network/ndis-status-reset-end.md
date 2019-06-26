---
title: NDIS_STATUS_RESET_END
description: NDIS_STATUS_RESET_END 状態では、ミニポート アダプターのリセット操作が完了したことを示します。
ms.assetid: 09ced263-9e4b-45e3-ae5e-db033a03b5b6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RESET_END ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d3b1b3ef2fe76e487bba8bbdcc72340b52782493
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385075"
---
# <a name="ndisstatusresetend"></a>NDIS\_状態\_リセット\_終了


NDIS\_状態\_リセット\_終了ステータスは、ミニポート アダプターのリセット操作が完了したことを示します。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーは呼び出さないでください、 [ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)関数開始を通知し、リセット操作の開始時に、NDIS が上にあるドライバーを通知するために各リセット操作の完了と終了します。

NDIS ミニポート ドライバーでは、リセット操作を開始、通知の上にあるドライバーを[ **NDIS\_状態\_リセット\_開始**](ndis-status-reset-start.md)状態を示す値。

バインドされているプロトコル後は、ドライバーは、NDIS を受け取ります。\_状態\_リセット\_終了ステータスを示す値、データを送信し、OID 要求を行う、プロトコルのドライバーを再開できます。

上位フィルターまたは中間ドライバーを受け取た後、NDIS\_状態\_リセット\_終了ステータスを示す値、データを送信して、ドライバーに関連する OID 要求を行う、ドライバーを再開できます。

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
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_リセット\_開始**](ndis-status-reset-start.md)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)

 

 




