---
title: WDI_TLV_PHY_DATA_RATE_LIST
description: WDI_TLV_PHY_DATA_RATE_LIST では、データ転送速度のリストを含む TLV です。
ms.assetid: FFD28866-4983-4C0B-A74D-4EF9A819571E
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_DATA_RATE_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ffb7fda3a5251da4926cbfad72a6c26a186fab39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373855"
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
| UINT8  | データで定義されているフラグを評価する[ **WDI\_データ\_レート\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_data_rate_flags)します。 |
| UINT16 | データ レートの値。                                                                          |

 

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

 

 




