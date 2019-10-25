---
title: WDI_TLV_ROAMING_NEEDED_PARAMETERS
description: WDI_TLV_ROAMING_NEEDED_PARAMETERS は、ローミングトリガーの理由を含む TLV です。 これは、NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED ペイロードで使用されます。
ms.assetid: 152F923C-ECAE-4D50-A7B4-4B2309D5A3B5
ms.date: 07/18/2017
keywords:
- WDI_TLV_ROAMING_NEEDED_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 0a982c9b75a30ca8dfd5da73845f90f506ebc480
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842271"
---
# <a name="wdi_tlv_roaming_needed_parameters"></a>WDI\_TLV\_ローミング\_必要な\_パラメーター


WDI\_TLV\_ローミング\_必要\_パラメーターは、ローミングトリガーの理由を含む TLV です。 これは、 [NDIS\_STATUS\_WDI\_](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)によって使用され、ローミング\_必要なペイロードが\_示されます。

## <a name="tlv-type"></a>TLV 型


0x55

## <a name="length"></a>Length


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| 種類                                                | 説明                                                                                                                                      |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ASSOC\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) | ローミングトリガーの理由を指定します。 [OID\_WDI\_タスク\_ローミング](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-roam)がトリガーされると、この理由が転送されます。 |

 

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最低限のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小サーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




