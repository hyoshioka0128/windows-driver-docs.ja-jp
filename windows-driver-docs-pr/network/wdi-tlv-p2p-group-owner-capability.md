---
title: WDI_TLV_P2P_GROUP_OWNER_CAPABILITY
description: WDI_TLV_P2P_GROUP_OWNER_CAPABILITY では、Wi-Fi Direct グループの所有者の機能情報を含む TLV です。
ms.assetid: 3F07665C-0212-465C-9118-CC213198EFB7
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GROUP_OWNER_CAPABILITY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2e2589209ff877e890b2b403206f6ac65b013c68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392187"
---
# <a name="wditlvp2pgroupownercapability"></a>WDI\_TLV\_P2P\_グループ\_所有者\_機能


WDI\_TLV\_P2P\_グループ\_所有者\_機能は、Wi-Fi Direct グループの所有者の機能情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x77

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8  | Wi-Fi Direct グループ機能に対応するビットマスクを指定します。 ビットマスクは、Wi-fi P2P technical specification 表 13 グループ機能のビットマップ定義で定義されているものと一致します。 |
| UINT8  | グループ機能ビットマップ上でオペレーティング システムによって設定するビットを指定します。                                                                                            |
| UINT32 | このグループの所有者のクライアントの最大数。                                                                                                                                      |

 

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

 

 




