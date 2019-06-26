---
title: WDI_TLV_ROAMING_NEEDED_PARAMETERS
description: WDI_TLV_ROAMING_NEEDED_PARAMETERS では、ローミングのトリガーの理由を含む TLV です。 これは、NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED ペイロードで使用されます。
ms.assetid: 152F923C-ECAE-4D50-A7B4-4B2309D5A3B5
ms.date: 07/18/2017
keywords:
- WDI_TLV_ROAMING_NEEDED_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fe9a7d94d8a37fc0d208c104400e197fd2b7300a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376983"
---
# <a name="wditlvroamingneededparameters"></a>WDI\_TLV\_ローミング\_必要\_パラメーター


WDI\_TLV\_ローミング\_必要\_パラメーターは、ローミングのトリガーの理由を含む TLV します。 使用されます、 [NDIS\_状態\_WDI\_INDICATION\_ローミング\_必要](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)ペイロード。

## <a name="tlv-type"></a>TLV 型


0x55

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                | 説明                                                                                                                                      |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ASSOC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_assoc_status) | ローミングのトリガーの理由を指定します。 ときに、 [OID\_WDI\_タスク\_ローミング](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-roam)がトリガーされると、この理由はそれに転送されます。 |

 

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

 

 




