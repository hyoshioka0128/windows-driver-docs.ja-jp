---
title: WDI_TLV_CIPHER_KEY_TKIP_INFO
description: WDI_TLV_CIPHER_KEY_TKIP_INFO では、[tkip] 情報を含む TLV です。
ms.assetid: 330A93F5-43E7-4A4A-A6BD-EF276D6F09A1
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_TKIP_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 610bf9bdaa365c5826b5ae869740204978aa2819
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574998"
---
# <a name="wditlvcipherkeytkipinfo"></a>WDI\_TLV\_暗号\_キー\_TKIP\_情報


WDI\_TLV\_暗号\_キー\_TKIP\_情報が [tkip] 情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x4B

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 型                                                                    | 許可されている複数の TLV インスタンス | 省略可能 | 説明                      |
|-------------------------------------------------------------------------|--------------------------------|----------|----------------------------------|
| [**WDI\_TLV\_暗号\_キー\_TKIP\_キー**](wdi-tlv-cipher-key-tkip-key.md) |                                |          | [Tkip] キー マテリアルを指定します。 |
| [**WDI\_TLV\_暗号\_キー\_TKIP\_MIC**](wdi-tlv-cipher-key-tkip-mic.md) |                                |          | [Tkip] MIC マテリアルを指定します。 |

 

<a name="requirements"></a>必要条件
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

 

 




