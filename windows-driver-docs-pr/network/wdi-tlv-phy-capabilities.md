---
title: WDI_TLV_PHY_CAPABILITIES
description: WDI_TLV_PHY_CAPABILITIES は、PHY 機能を含む TLV です。
ms.assetid: 8F482ED6-6594-4DB5-B53B-4424DAD32D36
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_CAPABILITIES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e57cf918a4916f08d497b43de94daa7d83f0570d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838017"
---
# <a name="wdi_tlv_phy_capabilities"></a>WDI\_TLV\_PHY\_の機能


WDI\_TLV\_PHY\_機能は、PHY 機能を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x1B

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                        | 説明                                        |
|---------------------------------------------|----------------------------------------------------|
| [**WDI\_PHY\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type) | PHY の種類を指定します。                           |
| UINT8                                       | PHY が CF ポーリングをサポートするかどうかを指定します。 |
| UINT32                                      | MPDU の最大長を指定します。                 |
| UINT32                                      | 動作温度クラスを指定します。         |
| UINT32                                      | アンテナ多様性サポートを指定します。           |

 

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

 

 




