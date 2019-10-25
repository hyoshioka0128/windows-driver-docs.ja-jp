---
title: WDI_TLV_IHV_TASK_REQUEST_PARAMETERS
description: WDI_TLV_IHV_TASK_REQUEST_PARAMETERS は、NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST に対して要求された優先度を含む TLV です。
ms.assetid: C33CF8FE-EDBC-41D1-A63C-E43650E9570E
ms.date: 07/18/2017
keywords:
- WDI_TLV_IHV_TASK_REQUEST_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 937aa7e1bd2445a30b884e98245e3586d3bcbded
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840385"
---
# <a name="wdi_tlv_ihv_task_request_parameters"></a>WDI\_TLV\_IHV\_タスク\_要求\_パラメーター


WDI\_TLV\_IHV\_タスク\_要求\_パラメーターは、 [NDIS\_STATUS\_WDI\_\_IHV\_TASK\_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-ihv-task-request)に対して要求された優先度を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xDF

## <a name="length"></a>長さ


UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに   | 説明                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | IHV が要求したこのタスクの優先順位。 有効な優先順位値については、「 [**WDI\_IHV\_TASK\_priority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ihv_task_priority) 」を参照してください。 |

 

<a name="requirements"></a>要件
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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




