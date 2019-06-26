---
title: WDI_TLV_IHV_TASK_REQUEST_PARAMETERS
description: WDI_TLV_IHV_TASK_REQUEST_PARAMETERS は、NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST の要求の優先度を含む TLV です。
ms.assetid: C33CF8FE-EDBC-41D1-A63C-E43650E9570E
ms.date: 07/18/2017
keywords:
- WDI_TLV_IHV_TASK_REQUEST_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 60a227b1c4a58f931d6e19e80e745abfbc956eb8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380790"
---
# <a name="wditlvihvtaskrequestparameters"></a>WDI\_TLV\_IHV\_タスク\_要求\_パラメーター


WDI\_TLV\_IHV\_タスク\_要求\_パラメーターが要求された優先度を含む TLV [NDIS\_状態\_WDI\_INDICATION\_IHV\_タスク\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-ihv-task-request)します。

## <a name="tlv-type"></a>TLV 型


0 xdf

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | このタスクの IHV から要求された優先順位。 参照してください[ **WDI\_IHV\_タスク\_優先度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ihv_task_priority)の有効な優先度の値。 |

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




