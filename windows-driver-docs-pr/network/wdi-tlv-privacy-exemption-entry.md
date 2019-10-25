---
title: WDI_TLV_PRIVACY_EXEMPTION_ENTRY
description: WDI_TLV_PRIVACY_EXEMPTION_ENTRY は、プライバシーに関する除外エントリを含む TLV です。
ms.assetid: 086BD366-F54C-4BF4-8544-CC2AB2472EB2
ms.date: 07/18/2017
keywords:
- WDI_TLV_PRIVACY_EXEMPTION_ENTRY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f733f6fffd3e397e7423a6854183f3942be70754
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844585"
---
# <a name="wdi_tlv_privacy_exemption_entry"></a>WDI\_TLV\_PRIVACY\_除外\_エントリ


WDI\_TLV\_PRIVACY\_除外\_エントリは、プライバシー除外エントリを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x48

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                   | 説明                                                 |
|------------------------------------------------------------------------|-------------------------------------------------------------|
| UINT16                                                                 | ビッグエンディアンのバイト順で IEEE EtherType を指定します。      |
| [**WDI\_除外\_アクション\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_exemption_action_type) | 除外対象のアクションの種類を指定します。                 |
| [**WDI\_除外\_パケット\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_exemption_packet_type) | 除外対象が適用されるパケットの種類を指定します。 |

 

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

 

 




