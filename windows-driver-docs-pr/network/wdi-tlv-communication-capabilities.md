---
title: WDI_TLV_COMMUNICATION_CAPABILITIES
description: WDI_TLV_COMMUNICATION_CAPABILITIES では、通信機能を指定する TLV です。
ms.assetid: 0A603358-05EA-4796-8D7F-E8F86F1C30F1
ms.date: 07/18/2017
keywords:
- WDI_TLV_COMMUNICATION_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e12e3367a119d9883b1e7fe1f1b741cd16393934
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577952"
---
# <a name="wditlvcommunicationcapabilities"></a>WDI\_TLV\_通信\_機能


WDI\_TLV\_通信\_機能は、TLV 通信機能を指定します。

## <a name="tlv-type"></a>TLV 型


0xE

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                        |
|--------|------------------------------------|
| UINT32 | コマンドの最大サイズ (バイト単位)。 |

 

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

 

 




