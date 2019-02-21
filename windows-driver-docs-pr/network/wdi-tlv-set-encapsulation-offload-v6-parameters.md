---
title: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS
description: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS では、IPv6 のオフロードを開始する必要があるかどうかを示す OID_WDI_SET_ENCAPSULATION_OFFLOAD で使用される TLV です。
ms.assetid: 7036AFD0-197E-4A94-8580-A42889BE6798
ms.date: 07/18/2017
keywords:
- WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 45e1bf94ba89aa9471bd6c396de2ffb21664f09f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539558"
---
# <a name="wditlvsetencapsulationoffloadv6parameters"></a>WDI\_TLV\_設定\_カプセル化\_オフロード\_V6\_パラメーター


WDI\_TLV\_設定\_カプセル化\_オフロード\_V6\_パラメーターで使用される TLV [OID\_WDI\_設定\_カプセル化\_オフロード](https://msdn.microsoft.com/library/windows/hardware/dn925930)を IPv6 のオフロードを開始する必要があるかどうかを示します。

## <a name="tlv-type"></a>TLV 型


0 xfe

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                                                                                                                             |
|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | IPv6 のオフロードを開始する必要があるかどうかを指定します。 NDIS にこの設定は\_オフロード\_設定\_ON を有効にして、NDIS に設定\_オフロード\_設定\_無効になっている場合はオフです。 |

 

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


[**NDIS\_オフロード\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

 

 




