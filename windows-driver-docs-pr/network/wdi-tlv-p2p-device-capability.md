---
title: WDI_TLV_P2P_DEVICE_CAPABILITY
description: WDI_TLV_P2P_DEVICE_CAPABILITY では、Wi-Fi Direct デバイス機能を含む TLV です。
ms.assetid: 490CA066-998F-4F15-AFC2-028299042496
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_CAPABILITY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 86d861b334849837f3df3531b075a3d77f311654
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552906"
---
# <a name="wditlvp2pdevicecapability"></a>WDI\_TLV\_P2P\_デバイス\_機能


WDI\_TLV\_P2P\_デバイス\_機能は、Wi-Fi Direct デバイス機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x84

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------|
| UINT8  | Wi-Fi Direct デバイスの Wi-Fi Direct technical specification 表 12 で定義されている機能のビットマップです。            |
| UINT8  | オペレーティング システムによって現在設定されている Wi-Fi Direct 機能上のデバイス機能ビットマップでのビットマップです。 |
| UINT32 | WPS バージョンが有効になっているかを示すビットマスク。                                                                        |

 

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

 

 




