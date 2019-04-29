---
title: WDI_TLV_IHV_DATA
description: WDI_TLV_IHV_DATA では、IHV 機能拡張のモジュールで使用される IHV 固有の情報を含む TLV です。
ms.assetid: 50D80D9E-C3FF-41E5-A054-A5A28ED499FD
ms.date: 07/18/2017
keywords:
- WDI_TLV_IHV_DATA ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b9a334edcc0ad4497b419e15057d6bd8769d8575
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392893"
---
# <a name="wditlvihvdata"></a>WDI\_TLV\_IHV\_データ


WDI\_TLV\_IHV\_データは、IHV 拡張モジュールで使用される IHV 固有の情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xBD

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                            |
|-----------|------------------------------------------------------------------------|
| UINT8\[\] | IHV 固有の情報、IHV 拡張モジュールで使用されます。 |

 

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

 

 




