---
title: WDI_TLV_ADAPTER_NLO_SCAN_MODE
description: WDI_TLV_ADAPTER_NLO_SCAN_MODE では、アクティブまたはパッシブ モードでスキャンを実行するかどうかを示す TLV です。
ms.assetid: 4294AF4D-587E-4978-9C54-E11D7368FBB8
ms.date: 07/18/2017
keywords:
- WDI_TLV_ADAPTER_NLO_SCAN_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 95dadeb161840e0e4d975d40c701159b3fa5147d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356815"
---
# <a name="wditlvadapternloscanmode"></a>WDI\_TLV\_アダプター\_NLO\_スキャン\_モード


WDI\_TLV\_アダプター\_NLO\_スキャン\_モードがアクティブまたはパッシブ モードでスキャンを実行するかどうかを示す TLV します。

## <a name="tlv-type"></a>TLV 型


0x125

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_スキャン\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926115)アクティブまたはパッシブ モードでスキャンを実行するかどうかを示す値です。 |

 

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

 

 




