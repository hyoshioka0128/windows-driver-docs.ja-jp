---
title: NDIS_STATUS_RESET_END
description: NDIS_STATUS_RESET_END 状態は、ミニポートアダプターのリセット操作が完了したことを示します。
ms.assetid: 09ced263-9e4b-45e3-ae5e-db033a03b5b6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RESET_END ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 7583fd7db8c73eae0009f2fd2e4477bab841e4bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843517"
---
# <a name="ndis_status_reset_end"></a>NDIS\_状態\_リセット\_終了


NDIS\_STATUS\_RESET\_END status は、ミニポートアダプターのリセット操作が完了したことを示します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、リセット操作の開始時と終了時に NDIS からドライバーに通知されるため、各リセット操作の開始と終了を通知するために[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数を呼び出すことはできません。

ミニポートドライバーがリセット操作を開始すると、NDIS は、前のドライバーに[**ndis\_状態を通知\_\_開始**](ndis-status-reset-start.md)状態の表示をリセットします。

バインドされたプロトコルドライバーが NDIS\_状態を受信した後\_終了状態を示す\_リセットすると、プロトコルドライバーはデータの送信を再開し、OID 要求を行うことができます。

その後のフィルターまたは中間ドライバーが NDIS\_STATUS を受け取った後\_終了状態を示す\_リセットすると、ドライバーはデータの送信を再開して、その後のドライバーに OID 要求を行うことができます。

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
<td><p>Windows Vista では、NDIS 6.0 および NDIS 5.1 ドライバーでサポートされています。 Windows XP の NDIS 5.1 ドライバーでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_リセット\_開始**](ndis-status-reset-start.md)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

 




