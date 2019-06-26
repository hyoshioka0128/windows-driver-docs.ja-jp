---
title: WDI_TLV_FT_PMKR0NAME
description: WDI_TLV_FT_PMKR0NAME PMKR0Name や PMKR1Name を含む TLV は、(802.11r)。
ms.assetid: F280FB10-D6CD-4410-8F3C-CD114F62B091
ms.date: 07/18/2017
keywords:
- WDI_TLV_FT_PMKR0NAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 346f274f32b1d79d1ba1e79d10765fd741bda3f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358537"
---
# <a name="wditlvftpmkr0name"></a>WDI\_TLV\_FT\_PMKR0NAME


WDI\_TLV\_FT\_PMKR0NAME PMKR0Name や PMKR1Name を含む TLV は、(802.11r)。

## <a name="tlv-type"></a>TLV 型


0x107

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_型\_PMK\_名前**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_type_pmk_name)構造体。

## <a name="values"></a>値


| 型                                                   | 説明                         |
|--------------------------------------------------------|-------------------------------------|
| [**WDI\_型\_PMK\_名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_type_pmk_name) | PMKR0Name または PMKR1Name (802.11r)。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




