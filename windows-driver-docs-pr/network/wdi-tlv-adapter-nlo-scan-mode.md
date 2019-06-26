---
title: WDI_TLV_ADAPTER_NLO_SCAN_MODE
description: WDI_TLV_ADAPTER_NLO_SCAN_MODE では、アクティブまたはパッシブ モードでスキャンを実行するかどうかを示す TLV です。
ms.assetid: 4294AF4D-587E-4978-9C54-E11D7368FBB8
ms.date: 07/18/2017
keywords:
- WDI_TLV_ADAPTER_NLO_SCAN_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1053924c720ee8f2cef3acec977e5660aa7f72c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381126"
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
| UINT32 | [**WDI\_スキャン\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_scan_type)アクティブまたはパッシブ モードでスキャンを実行するかどうかを示す値です。 |

 

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

 

 




