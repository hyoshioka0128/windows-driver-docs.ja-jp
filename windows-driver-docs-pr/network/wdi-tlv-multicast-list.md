---
title: WDI_TLV_MULTICAST_LIST
description: WDI_TLV_MULTICAST_LIST は、マルチキャスト MAC アドレスの配列を含む TLV です。
ms.assetid: 5023557A-1BC5-4A4E-A77C-20353C0CA3FD
ms.date: 07/18/2017
keywords:
- WDI_TLV_MULTICAST_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 9e634598f6e530ec85582a8f2a7457e58d1b1697
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844982"
---
# <a name="wdi_tlv_multicast_list"></a>WDI\_TLV\_マルチキャスト\_一覧


WDI\_TLV\_マルチキャスト\_リストは、マルチキャスト MAC アドレスの配列を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x6A

## <a name="length"></a>長さ


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体の配列のサイズ (バイト単位)。 配列には1つ以上の構造体が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                  | 説明                          |
|-------------------------------------------------------|--------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | マルチキャスト MAC アドレスの配列。 |

 

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

 

 




