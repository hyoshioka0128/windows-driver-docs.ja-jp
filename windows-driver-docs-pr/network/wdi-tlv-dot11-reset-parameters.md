---
title: WDI_TLV_DOT11_RESET_PARAMETERS
description: WDI_TLV_DOT11_RESET_PARAMETERS は、OID_WDI_TASK_DOT11_RESET のパラメーターを含む TLV です。
ms.assetid: 14F3DECD-E875-44BB-969B-705B075E4636
ms.date: 07/18/2017
keywords:
- WDI_TLV_DOT11_RESET_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: acafb7853668961d8e866f6c248d7faee80d9028
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559456"
---
# <a name="wditlvdot11resetparameters"></a>WDI\_TLV\_DOT11\_リセット\_パラメーター


WDI\_TLV\_DOT11\_リセット\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_DOT11\_のリセット](https://msdn.microsoft.com/library/windows/hardware/dn925952).

## <a name="tlv-type"></a>TLV 型


0xA2

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                                                                                     |
|-------|-----------------------------------------------------------------------------------------------------------------|
| UINT8 | 場合 (および場合にのみ) 1 に設定されて、その既定値にリセットされるポートのすべての MIB 属性が設定されます。 |

 

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

 

 




