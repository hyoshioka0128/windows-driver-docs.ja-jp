---
title: WDI_TLV_FT_REASSOC_PARAMETERS
description: WDI_TLV_FT_REASSOC_PARAMETERS では、高速の遷移の再関連付けパラメーターを含む TLV です。
ms.assetid: 36F260FF-E80A-4EFF-B009-B06446229470
ms.date: 07/18/2017
keywords:
- WDI_TLV_FT_REASSOC_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 68f27c22888b4c9c53a66217bfbad87648335c86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551713"
---
# <a name="wditlvftreassocparameters"></a>WDI\_TLV\_FT\_REASSOC\_パラメーター


WDI\_TLV\_FT\_REASSOC\_パラメーターは、高速の遷移の再関連付けパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x106

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                                    | 説明                                                                                                                            |
|---------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_FT\_MDE**](wdi-tlv-ft-mde.md)             | BSS エントリの MDIE します。                                                                                                             |
| [**WDI\_TLV\_FT\_PMKR0NAME**](wdi-tlv-ft-pmkr0name.md) | PMKR0Name します。 これは、高速の遷移中に必要です。 STA は、認証要求時に、ap、PMKR0Name を送信する必要があります。 |
| [**WDI\_TLV\_FT\_FTE**](wdi-tlv-ft-fte.md)             | 高速切り替え要素 R0KHID および SNonce を格納します。                                                                       |

 

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

 

 




