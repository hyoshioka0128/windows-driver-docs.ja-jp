---
title: NDIS_STATUS_WWAN_PRESHUTDOWN_STATE
description: NDIS_STATUS_WWAN_PRESHUTDOWN_STATE 通知は、MBB ドライバーからホストへの一方向の通知です。
ms.assetid: 191629A1-2BBF-42D8-A053-827222CE35B0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_PRESHUTDOWN_STATE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 502c41abbdd3471e49d7a822141304ba63731353
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844695"
---
# <a name="ndis_status_wwan_preshutdown_state"></a>NDIS\_ステータス\_WWAN\_プレシャットダウン\_状態


NDIS\_ステータス\_WWAN\_PRESHUTDOWN\_状態通知は、MBB ドライバーからホストへの一方向の通知です。 MBB ドライバーは、シャットダウン前に必要なすべての操作がモデムによって完了したときに、この通知を送信します。

この通知では、 [**NDIS\_WWAN\_PRESHUTDOWN\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preshutdown_state)構造体を使用します。

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
<td><p>Windows 10 バージョン1511以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

 

 




