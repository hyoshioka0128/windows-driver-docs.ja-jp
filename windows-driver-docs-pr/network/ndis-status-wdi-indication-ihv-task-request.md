---
title: NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST
description: ミニポートドライバーは、NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST を使用して、Microsoft コンポーネントが IHV タスクをキューに要求します。ObjectPort。
ms.assetid: E123F957-574F-4C78-B366-76E886018503
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 151e2a75cca57edbde7a60a7149042d40bda910b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843461"
---
# <a name="ndis_status_wdi_indication_ihv_task_request"></a>NDIS\_STATUS\_WDI\_指示\_IHV\_TASK\_REQUEST


ミニポートドライバーは、NDIS\_STATUS\_WDI\_の\_\_指示を使用して、Microsoft コンポーネントが IHV タスクをキューに要求するように要求します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロードデータ


| タスクバーの検索ボックスに                                                                                         | 複数の TLV インスタンスを使用できます | オプション | 説明                                                                                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_IHV\_タスク\_要求\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-task-request-parameters) |                                |          | IHV が要求したこのタスクの優先順位。 有効な値については、 [**WDI\_IHV\_タスク\_PRIORITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ihv_task_priority)列挙を参照してください。 |
| [**WDI\_TLV\_IHV\_タスク\_デバイス\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ihv-task-device-context)         |                                | X        | [OID\_WDI\_タスク\_ihv](oid-wdi-task-ihv.md)に転送される ihv 提供のコンテキスト情報。                                       |

 

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_タスク\_IHV](oid-wdi-task-ihv.md)

 

 




