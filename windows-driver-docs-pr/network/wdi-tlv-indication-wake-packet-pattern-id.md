---
title: WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID
description: WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID では、ウェイク アップ パケットに一致するパターンの ID を含む TLV です。
ms.assetid: 3E1D4CC4-0369-4C1F-94C6-AFC34C861E0D
ms.date: 07/18/2017
keywords:
- WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 35d662515dd2449077a176e92919b00104386a49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548705"
---
# <a name="wditlvindicationwakepacketpatternid"></a>WDI\_TLV\_INDICATION\_WAKE\_パケット\_パターン\_ID


WDI\_TLV\_INDICATION\_WAKE\_パケット\_パターン\_ID がウェイク アップ パケットに一致するパターンの ID を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xB0

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                                                                    |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | ウェイク アップ パケットに一致するパターンの ID。 使用パターンが追加されたときに、ID が定義されて[OID\_WDI\_設定\_追加\_WOL\_パターン](https://msdn.microsoft.com/library/windows/hardware/dn925858)します。 |

 

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

 

 




