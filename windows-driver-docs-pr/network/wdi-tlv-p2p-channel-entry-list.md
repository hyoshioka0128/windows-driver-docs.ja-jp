---
title: WDI_TLV_P2P_CHANNEL_ENTRY_LIST
description: WDI_TLV_P2P_CHANNEL_ENTRY_LIST では、チャネル番号のリストを含む TLV です。
ms.assetid: 10739684-C00C-4AE7-A3B2-D4A6F1E9829B
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CHANNEL_ENTRY_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dd4a9ad8ba318cf8023aed75c3faab14b4a1aac1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527229"
---
# <a name="wditlvp2pchannelentrylist"></a>WDI\_TLV\_P2P\_チャネル\_エントリ\_一覧


WDI\_TLV\_P2P\_チャネル\_エントリ\_リストは、チャネル番号のリストを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xF9

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                          |
|--------------------------------------------------------------------|--------------------------------|----------|--------------------------------------|
| [**WDI\_TLV\_オペレーティング\_クラス**](wdi-tlv-operating-class.md)      |                                |          | チャネルの周波数帯。 |
| [**WDI\_TLV\_チャネル\_情報\_一覧**](wdi-tlv-channel-info-list.md) |                                |          | チャネル番号のリスト。             |

 

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

 

 




