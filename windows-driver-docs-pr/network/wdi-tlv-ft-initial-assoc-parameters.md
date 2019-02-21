---
title: WDI_TLV_FT_INITIAL_ASSOC_PARAMETERS
description: WDI_TLV_FT_INITIAL_ASSOC_PARAMETERS では、高速切り替えの最初の関連付けのパラメーターを含む TLV です。
ms.assetid: 3A91AC2F-5654-488D-89A5-36A0AC71A836
ms.date: 07/18/2017
keywords:
- WDI_TLV_FT_INITIAL_ASSOC_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 782444cc7ff6dd28f3e8e7aab46a4ca996e3294a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538666"
---
# <a name="wditlvftinitialassocparameters"></a>WDI\_TLV\_FT\_初期\_ASSOC\_パラメーター


WDI\_TLV\_FT\_初期\_ASSOC\_パラメーターは、高速切り替えの最初の関連付けのパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x105

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                        | 説明                |
|---------------------------------------------|----------------------------|
| [**WDI\_TLV\_FT\_MDE**](wdi-tlv-ft-mde.md) | BSS エントリの MDIE します。 |

 

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

 

 




