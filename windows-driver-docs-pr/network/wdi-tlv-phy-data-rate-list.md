---
title: WDI_TLV_PHY_DATA_RATE_LIST
description: WDI_TLV_PHY_DATA_RATE_LIST は、データレートの一覧を含む TLV です。
ms.assetid: FFD28866-4983-4C0B-A74D-4EF9A819571E
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_PHY_DATA_RATE_LIST
ms.localizationpriority: medium
ms.openlocfilehash: 0b91d79caa6614493e4a67f2f6b530a6e6bdcd60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838016"
---
# <a name="wdi_tlv_phy_data_rate_list"></a>WDI\_TLV\_PHY\_データ\_レート\_一覧


WDI\_TLV\_PHY\_データ\_レート\_一覧は、データレートの一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x13

## <a name="length"></a>長さ


WDI の配列のサイズ (バイト単位)\_リストの要素の\_データ\_レート。 配列には1つ以上の要素が含まれている必要があります。

**注**  WDI\_データ\_率\_リストは、WDI 構造体ではありません。 これは、WDI TLV parser ジェネレーターで定義されており、ドキュメントの目的でのみ使用されます。

 

## <a name="values"></a>値


| 種類                      | 説明                                                                                             |
|---------------------------|---------------------------------------------------------------------------------------------------------|
| WDI\_DATA\_RATE\_LIST\[\] | データ速度の配列。 配列内の各データレートには、データレートフラグとデータレート値が含まれている必要があります。 |

 

WDI\_DATA\_RATE\_リストは、次の要素で構成されています。

| 種類   | 説明                                                                                   |
|--------|-----------------------------------------------------------------------------------------------|
| UINT8  | [**WDI\_data\_rate\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_data_rate_flags)に定義されているデータレートフラグ。 |
| UINT16 | データ速度の値。                                                                          |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




