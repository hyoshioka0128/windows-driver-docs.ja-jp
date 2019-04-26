---
title: WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST
description: WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST では、マルチキャスト データ アルゴリズム ペアの配列を含む TLV です。
ms.assetid: BF07170E-CF4E-4E93-85E1-3276E414BDD9
ms.date: 07/18/2017
keywords:
- WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bc97015c4885a5becd1f3d90f5ae8173343682a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342917"
---
# <a name="wditlvmulticastdataalgorithmlist"></a>WDI\_TLV\_マルチキャスト\_データ\_アルゴリズム\_一覧


WDI\_TLV\_マルチキャスト\_データ\_アルゴリズム\_リストは、マルチキャスト データ アルゴリズム ペアの配列を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x14

## <a name="length"></a>長さ


WDI の配列のサイズをバイト単位で\_ALGO\_ペア要素。 配列には、1 つ以上の要素を含める必要があります。

**注**  WDI\_ALGO\_ペアが WDI 構造ではありません。 WDI TLV パーサー ジェネレーターで定義されているし、ドキュメントの目的でのみ使用されます。

 

## <a name="values"></a>値


| 型                 | 説明                                            |
|----------------------|--------------------------------------------------------|
| WDI\_ALGO\_ペア\[\] | 認証と暗号アルゴリズムのペアの配列。 |

 

WDI\_ALGO\_ペアは、次の要素で構成されます。

| 種類  | 説明                                                                                     |
|-------|-------------------------------------------------------------------------------------------------|
| UINT8 | 定義されている認証アルゴリズム[ **WDI\_AUTH\_アルゴリズム**](https://msdn.microsoft.com/library/windows/hardware/dn897792)します。 |
| UINT8 | 定義されている暗号アルゴリズム[ **WDI\_暗号\_アルゴリズム**](https://msdn.microsoft.com/library/windows/hardware/dn897802)します。     |

 

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

 

 




