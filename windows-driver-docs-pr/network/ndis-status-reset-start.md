---
title: NDIS_STATUS_RESET_START
description: NDIS_STATUS_RESET_START の状態は、ミニポートアダプターがリセットされていることを示します。
ms.assetid: 8758652b-137b-43e3-a896-8360f2b5051c
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RESET_START ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 2c0a22f0fec7b6921edbd79195d271d28b59baa9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843515"
---
# <a name="ndis_status_reset_start"></a>NDIS\_状態\_リセット\_開始


NDIS\_STATUS\_RESET\_START status は、ミニポートアダプターがリセットされていることを示します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、リセット操作の開始時と終了時に NDIS からドライバーに通知されるため、各リセット操作の開始と終了を通知するために[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数を呼び出すことはできません。

ミニポートドライバーは、NDIS がミニポートドライバーの[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数を呼び出すと、ミニポートアダプターをリセットします。 NDIS は、バインドされている各プロトコルと中間ドライバーの[*Protocolstatusex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)関数、およびその後のフィルターモジュールの[*filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数を呼び出します。状態は NDIS\_STATUS\_リセット\_開始されます。 ミニポートドライバーによってリセットが完了すると、NDIS は、前のドライバーに対して、 [**ndis\_status の状態\_リセット\_終了**](ndis-status-reset-end.md)を通知します。

プロトコルドライバーが NDIS\_の状態を受信し\_開始状態の通知\_リセットした場合、次のことを行う必要があります。

-   *Protocolstatusex*関数が NDIS\_status を受け取るまで、送信する準備ができているすべてのデータを保持し\_終了状態の通知\_リセットします。

-   基になるミニポートドライバーに送信される NDIS 呼び出しを行わないでください。ただし、 [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)関数を使用して受信したデータバッファーなどのリソースを返す呼び出しは除きます。

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


[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)

[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)

[**NDIS\_状態\_リセット\_終了**](ndis-status-reset-end.md)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)

[*ProtocolStatusEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)

 

 




