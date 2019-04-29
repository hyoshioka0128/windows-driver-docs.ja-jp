---
title: WDI_TLV_OPERATING_CLASS
description: WDI_TLV_OPERATING_CLASS では、チャネルの周波数帯域を含む TLV です。
ms.assetid: 58F2D174-EB47-4163-AFFD-C119E5E7CE53
ms.date: 07/18/2017
keywords:
- WDI_TLV_OPERATING_CLASS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4bc8b17b88df12cf2cf52d2d9cf4ead47fbe6312
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385258"
---
# <a name="wditlvoperatingclass"></a>WDI\_TLV\_オペレーティング\_クラス


WDI\_TLV\_オペレーティング\_クラスは、チャネルの周波数帯域を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xFA

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 型  | 説明                       |
|-------|-----------------------------------|
| UINT8 | チャネルの周波数帯。 |

 

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

 

 




