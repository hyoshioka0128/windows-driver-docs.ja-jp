---
title: WDI_TLV_AUTH_ALGO_LIST
description: WDI_TLV_AUTH_ALGO_LIST では、認証アルゴリズムの一覧を含む TLV です。
ms.assetid: 6F5EC21B-C923-45ED-B62E-302D916AABE5
ms.date: 07/18/2017
keywords:
- WDI_TLV_AUTH_ALGO_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 12d031cd5c6b0e898ef7f1206103947f8dd8f4eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361801"
---
# <a name="wditlvauthalgolist"></a>WDI\_TLV\_AUTH\_ALGO\_一覧


WDI\_TLV\_AUTH\_ALGO\_リストは、認証アルゴリズムの一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x3c です.

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_AUTH\_アルゴリズム**](https://msdn.microsoft.com/library/windows/hardware/dn897792)構造体。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型                                                        | 説明                            |
|-------------------------------------------------------------|----------------------------------------|
| [**WDI\_AUTH\_アルゴリズム**](https://msdn.microsoft.com/library/windows/hardware/dn897792)\[\] | 認証アルゴリズムの配列。 |

 

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

 

 




