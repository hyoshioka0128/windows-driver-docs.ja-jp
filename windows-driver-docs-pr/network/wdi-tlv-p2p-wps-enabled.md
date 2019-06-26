---
title: WDI_TLV_P2P_WPS_ENABLED
description: WDI_TLV_P2P_WPS_ENABLED では、Wi-fi 保護設定が有効かどうかを示す TLV です。
ms.assetid: B923DA17-451C-4BF1-8B8B-C2846EDE9774
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_WPS_ENABLED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2f17406ff0b7c638d95b0131903a8805eeb7e300
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385413"
---
# <a name="wditlvp2pwpsenabled"></a>WDI\_TLV\_P2P\_WPS\_有効


WDI\_TLV\_P2P\_WPS\_Wi-fi 保護設定が有効かどうかを示す TLV されます。

## <a name="tlv-type"></a>TLV 型


0xF7

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>Wi-fi 保護設定が有効になっているかどうかを指定します。
<p>有効な値は 0 (無効) および 1 (有効です)。</p></td>
</tr>
</tbody>
</table>

 

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

## <a name="see-also"></a>関連項目


[OID\_WDI\_SET\_P2P\_WPS\_ENABLED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-p2p-wps-enabled)

 

 




