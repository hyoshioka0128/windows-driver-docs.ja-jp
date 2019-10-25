---
title: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS
description: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS は、NDIS_STATUS_WDI_INDICATION_DISASSOCIATION の関連付けを示すパラメーターを含む TLV です。
ms.assetid: AD799DAA-B89D-4015-8DC5-53057C4DA43E
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: d1bdd2e7f2b3350da6be78c9d92c2449ba0d016b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834140"
---
# <a name="wdi_tlv_disassociation_indication_parameters"></a>WDI\_TLV\_関連付け\_示さ\_パラメーター


WDI\_TLV\_関連付け\_示さ\_パラメーターは、 [NDIS\_STATUS\_関連付け\_](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-disassociation)\_WDI を示す関連付けを示すパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xBC

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                         | 説明                                                                |
|--------------------------------------------------------------|----------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)            | 関連付けに関連付けられているピアの MAC アドレス。 |
| [**WDI\_ASSOC\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) (UINT32) | 関連付けを示すトリガー。                             |

 

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

 

 




