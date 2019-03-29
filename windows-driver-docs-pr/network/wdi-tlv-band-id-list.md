---
title: WDI_TLV_BAND_ID_LIST
description: WDI_TLV_BAND_ID_LIST では、バンド Id の一覧を含む TLV です。
ms.assetid: 415EF9E3-9441-420D-AC8A-0F819369E20E
ms.date: 07/18/2017
keywords:
- WDI_TLV_BAND_ID_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ea968a46b67a86d57aaf695cd63c7aa959870f2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580554"
---
# <a name="wditlvbandidlist"></a>WDI\_TLV\_バンド\_ID\_一覧


WDI\_TLV\_バンド\_ID\_リストは、バンド Id の一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xB6

## <a name="length"></a>長さ


WDI の配列のサイズをバイト単位で\_バンド\_要素 ID (UINT32)。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型              | 説明           |
|-------------------|-----------------------|
| WDI\_バンド\_ID\[\] | バンド Id の配列。 |

 

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

 

 




