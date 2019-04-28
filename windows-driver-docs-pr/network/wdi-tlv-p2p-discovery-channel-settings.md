---
title: WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS
description: WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS では、Wi-Fi Direct 検出チャネル設定を含む TLV です。
ms.assetid: 50BD3F70-4C12-4984-8E3F-AEC9F5C3CDCA
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DISCOVERY_CHANNEL_SETTINGS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c2b2dbe8ebd052196883ddea5cbf1e3500129f10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362486"
---
# <a name="wditlvp2pdiscoverychannelsettings"></a>WDI\_TLV\_P2P\_検出\_チャネル\_設定


WDI\_TLV\_P2P\_検出\_チャネル\_設定は、Wi-Fi Direct 検出チャネル設定を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xE8

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                         |
|------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_P2P\_リッスン\_期間**](wdi-tlv-p2p-listen-duration.md) |                                |          | サイクルの期間と待機時間。 |
| [**WDI\_TLV\_バンド\_チャネル**](wdi-tlv-band-channel.md)                | x                              |          | スキャンするチャネルのリスト。       |

 

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

 

 




