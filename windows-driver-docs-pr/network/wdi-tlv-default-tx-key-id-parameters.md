---
title: WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS
description: WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS は既定値を含む TLV OID_WDI_SET_DEFAULT_KEY_ID のポートのパケット転送のキー ID。
ms.assetid: 24E7E758-FEED-4D2A-BAA8-6DBC08726FBA
ms.date: 07/18/2017
keywords:
- WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 78253d0e03cbebc534ac0bc64b455cc3b5b8e74d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536909"
---
# <a name="wditlvdefaulttxkeyidparameters"></a>WDI\_TLV\_既定\_TX\_キー\_ID\_パラメーター


WDI\_TLV\_既定\_TX\_キー\_ID\_パラメーターが既定値を含む TLV パケット転送用のポートでのキー ID [OID\_WDI\_設定\_既定\_キー\_ID](https://msdn.microsoft.com/library/windows/hardware/dn925928)します。

## <a name="tlv-type"></a>TLV 型


0x54

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                     |
|--------|-----------------------------------------------------------------|
| UINT32 | 既定値を指定します。 パケットの送信ポートでのキー ID。 |

 

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

 

 




