---
title: WDI_TLV_PACKET_FILTER_PARAMETERS
description: WDI_TLV_PACKET_FILTER_PARAMETERS は、OID_WDI_SET_RECEIVE_PACKET_FILTER のパケット フィルター パラメーターを含む TLV です。
ms.assetid: 5B26DA60-BC5D-4CC5-A620-C076CECF22C0
ms.date: 07/18/2017
keywords:
- WDI_TLV_PACKET_FILTER_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dbd75422df1cb7dad11058eecd90245232412ec4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559086"
---
# <a name="wditlvpacketfilterparameters"></a>WDI\_TLV\_パケット\_フィルター\_パラメーター


WDI\_TLV\_パケット\_フィルター\_パラメーターは、のパケット フィルター パラメーターを含む TLV [OID\_WDI\_設定\_受信\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/dn925942)します。

## <a name="tlv-type"></a>TLV 型


0x47

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類                                                                      | 説明                                |
|---------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_パケット\_フィルター\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926104) (UINT32) | 必要な Wi-fi パケット フィルターを指定します。 |

 

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

 

 




