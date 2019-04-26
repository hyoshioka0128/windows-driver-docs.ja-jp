---
title: WDI_TLV_LSO_V2_CAPABILITIES
description: WDI_TLV_LSO_V2_CAPABILITIES では、大規模なオフロード V2 の送信機能を含む TLV です。
ms.assetid: 6F7C83BA-B004-431F-90AF-AD7DE1B13546
ms.date: 07/18/2017
keywords:
- WDI_TLV_LSO_V2_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4d9aae61f669f84c60f44efa0301ddb4d939fcc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357250"
---
# <a name="wditlvlsov2capabilities"></a>WDI\_TLV\_LSO\_V2\_機能


WDI\_TLV\_LSO\_V2\_機能は、大規模なオフロード V2 の送信機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xCD

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                  |
|--------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI\_TLV\_IPV4\_LSO\_V2**](wdi-tlv-ipv4-lso-v2.md) |                                |          | IPv4 の大規模なオフロード V2 の送信機能。 |
| [**WDI\_TLV\_IPV6\_LSO\_V2**](wdi-tlv-ipv6-lso-v2.md) |                                |          | IPv6 の大規模なオフロード V2 の送信機能。 |

 

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

 

 




