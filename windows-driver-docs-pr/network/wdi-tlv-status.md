---
title: WDI_TLV_STATUS
description: WDI_TLV_STATUS では、状態値を含む TLV です。
ms.assetid: 62A331EB-5765-41E9-A1CC-0CFF69BC4EF3
ms.date: 07/18/2017
keywords:
- WDI_TLV_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 616f2b0dfb4c0c82bcab72004819d6b0c46fef29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579605"
---
# <a name="wditlvstatus"></a>WDI\_TLV\_状態


WDI\_TLV\_状態が状態の値を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x1

## <a name="length"></a>長さ


サイズ (バイト単位)、NDIS の\_状態。

## <a name="values"></a>値


| 型         | 説明             |
|--------------|-------------------------|
| NDIS\_状態 | NDIS\_状態値。 |

 

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

 

 




