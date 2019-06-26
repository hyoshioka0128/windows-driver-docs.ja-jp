---
title: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS
description: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS は、NDIS_STATUS_WDI_INDICATION_DISASSOCIATION の関連付けの解除を示す値のパラメーターを含む TLV です。
ms.assetid: AD799DAA-B89D-4015-8DC5-53057C4DA43E
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 346b0005a76203a8b9c68a8b61feba0394650055
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360235"
---
# <a name="wditlvdisassociationindicationparameters"></a>WDI\_TLV\_戻せません\_INDICATION\_パラメーター


WDI\_TLV\_関連付け解除\_INDICATION\_パラメーターがの関連付けの解除を示す値のパラメーターを含む TLV [NDIS\_状態\_WDI\_INDICATION\_戻せません](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-disassociation)します。

## <a name="tlv-type"></a>TLV 型


0xBC

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                         | 説明                                                                |
|--------------------------------------------------------------|----------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)            | 関連付けの解除の指示に関連付けられているピアの MAC アドレス。 |
| [**WDI\_ASSOC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_assoc_status) (UINT32) | 関連付けの解除を示す値をトリガーします。                             |

 

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

 

 




