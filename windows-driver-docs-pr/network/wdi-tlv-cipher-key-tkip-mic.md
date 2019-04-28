---
title: WDI_TLV_CIPHER_KEY_TKIP_MIC
description: WDI_TLV_CIPHER_KEY_TKIP_MIC は、TKIP MIC マテリアルを含む TLV です。
ms.assetid: 5F1AE81C-6AB4-468C-9DEE-D1BB16A2EC4D
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_TKIP_MIC ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cace5ddd168aa7799677bfe59e3a474e8ebe382d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380558"
---
# <a name="wditlvcipherkeytkipmic"></a>WDI\_TLV\_暗号\_キー\_TKIP\_MIC


WDI\_TLV\_暗号\_キー\_TKIP\_MIC は TKIP MIC マテリアルを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x4A

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                      |
|-----------|------------------------------------------------------------------|
| UINT8\[\] | [Tkip] MIC マテリアルを指定する UINT8 要素の配列。 |

 

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

 

 




