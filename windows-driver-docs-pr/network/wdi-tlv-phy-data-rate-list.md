---
title: WDI_TLV_PHY_DATA_RATE_LIST
description: WDI_TLV_PHY_DATA_RATE_LIST では、データ転送速度のリストを含む TLV です。
ms.assetid: FFD28866-4983-4C0B-A74D-4EF9A819571E
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_DATA_RATE_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2b22840cac4183b268d79bbba4de7a84e72b2a72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377214"
---
# <a name="wditlvphydataratelist"></a>WDI\_TLV\_PHY\_データ\_レート\_一覧


WDI\_TLV\_PHY\_データ\_レート\_リストは、データ転送速度のリストを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x13

## <a name="length"></a>長さ


WDI の配列のサイズをバイト単位で\_データ\_レート\_リストの要素。 配列には、1 つ以上の要素を含める必要があります。

**注**  WDI\_データ\_レート\_一覧が WDI 構造ではありません。 WDI TLV パーサー ジェネレーターで定義されているし、ドキュメントの目的でのみ使用されます。

 

## <a name="values"></a>値


| 型                      | 説明                                                                                             |
|---------------------------|---------------------------------------------------------------------------------------------------------|
| WDI\_データ\_レート\_一覧\[\] | データ転送速度の配列。 配列内の各データ速度は、データ レート フラグとデータ レートの値を含める必要があります。 |

 

WDI\_データ\_レート\_リストは、次の要素で構成されます。

| 種類   | 説明                                                                                   |
|--------|-----------------------------------------------------------------------------------------------|
| UINT8  | データで定義されているフラグを評価する[ **WDI\_データ\_レート\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/dn897811)します。 |
| UINT16 | データ レートの値。                                                                          |

 

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

 

 




