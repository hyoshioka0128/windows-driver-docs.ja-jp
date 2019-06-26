---
title: WDI_TLV_CHANNEL_LIST
description: WDI_TLV_CHANNEL_LIST では、1 つまたは複数のチャンネル番号を含む TLV です。
ms.assetid: DBBA28C2-D80F-409B-BEE6-81B6FEDF7484
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHANNEL_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ef0bb6f30d9753ee2d3d17ec8dc7f35675301eb3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387203"
---
# <a name="wditlvchannellist"></a>WDI\_TLV\_チャネル\_一覧


WDI\_TLV\_チャネル\_リストは、1 つまたは複数のチャンネル番号を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x4

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_チャネル\_マッピング\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_channel_mapping_entry)構造体。 配列には、1 つ以上の構造を格納する必要があります。

## <a name="values"></a>値


| 型                                                                       | 説明                          |
|----------------------------------------------------------------------------|--------------------------------------|
| [**WDI\_チャネル\_マッピング\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_channel_mapping_entry)\[\] | チャネル マッピング エントリの配列。 |

 

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

 

 




