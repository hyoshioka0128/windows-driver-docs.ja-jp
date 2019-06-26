---
title: WDI_TLV_PHY_CAPABILITIES
description: WDI_TLV_PHY_CAPABILITIES は、PHY 機能を含む TLV です。
ms.assetid: 8F482ED6-6594-4DB5-B53B-4424DAD32D36
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3afd89398b3be938b26b65a2f6a6ed7fc2eceefd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385063"
---
# <a name="wditlvphycapabilities"></a>WDI\_TLV\_PHY\_機能


WDI\_TLV\_PHY\_機能は PHY 機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x1B

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                        | 説明                                        |
|---------------------------------------------|----------------------------------------------------|
| [**WDI\_PHY\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_phy_type) | PHY 型を指定します。                           |
| UINT8                                       | PHY が CF ポーリングをサポートしているかどうかを指定します。 |
| UINT32                                      | MPDU の最大長を指定します。                 |
| UINT32                                      | 動作の温度クラスを指定します。         |
| UINT32                                      | アンテナの多様性のサポートを指定します。           |

 

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

 

 




