---
title: WDI_TLV_CHANNEL_LIST
description: WDI_TLV_CHANNEL_LIST は、1つまたは複数のチャネル番号を含む TLV です。
ms.assetid: DBBA28C2-D80F-409B-BEE6-81B6FEDF7484
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHANNEL_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: eb2ba3fe2be6f79bb71b14733ab1a0796ff3beea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844523"
---
# <a name="wdi_tlv_channel_list"></a>WDI\_TLV\_CHANNEL\_LIST


WDI\_TLV\_CHANNEL\_LIST は、1つまたは複数のチャネル番号を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x4

## <a name="length"></a>長さ


WDI\_チャネルの配列のサイズ (バイト単位)。 [ **\_エントリ構造\_マッピング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_channel_mapping_entry)します。 配列には1つ以上の構造体が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                       | 説明                          |
|----------------------------------------------------------------------------|--------------------------------------|
| [**WDI\_CHANNEL\_マッピング\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_channel_mapping_entry)\[\] | チャネルマッピングエントリの配列。 |

 

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

 

 




