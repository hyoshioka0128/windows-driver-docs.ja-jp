---
title: WDI_TLV_UNICAST_ALGORITHM_LIST
description: WDI_TLV_UNICAST_ALGORITHM_LIST では、ユニキャスト データ アルゴリズム ペアの配列を含む TLV です。
ms.assetid: E216BE6A-5425-498F-ABDE-1229170DA5DB
ms.date: 07/18/2017
keywords:
- WDI_TLV_UNICAST_ALGORITHM_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b5351e1998506075789ccfe78d12b2380ac01ccb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530881"
---
# <a name="wditlvunicastalgorithmlist"></a>WDI\_TLV\_ユニキャスト\_アルゴリズム\_一覧


WDI\_TLV\_ユニキャスト\_アルゴリズム\_リストは、ユニキャスト データ アルゴリズム ペアの配列を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x13

## <a name="length"></a>長さ


WDI の配列のサイズをバイト単位で\_ALGO\_ペア要素。 配列には、1 つ以上の要素を含める必要があります。

**注**  WDI\_ALGO\_ペアが WDI 構造ではありません。 WDI TLV パーサー ジェネレーターで定義されているし、ドキュメントの目的でのみ使用されます。

 

## <a name="values"></a>値


| 種類                 | 説明                                            |
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

 

 




