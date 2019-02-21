---
title: WDI_TLV_BAND_CAPABILITIES
description: WDI_TLV_BAND_CAPABILITIES では、バンドの機能を含む TLV です。
ms.assetid: ABD198FE-8E81-4AF3-BB3D-D78AEB75782F
ms.date: 07/18/2017
keywords:
- WDI_TLV_BAND_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 695da6614b6b6025d6b9e82883878ad13b3fed60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536908"
---
# <a name="wditlvbandcapabilities"></a>WDI\_TLV\_バンド\_機能


WDI\_TLV\_バンド\_機能は、バンドの機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x1A

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                   |
|--------|-----------------------------------------------|
| UINT32 | バンドの識別子。                  |
| UINT8  | バンドが有効か無効かどうかを指定します。 |

 

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

 

 




