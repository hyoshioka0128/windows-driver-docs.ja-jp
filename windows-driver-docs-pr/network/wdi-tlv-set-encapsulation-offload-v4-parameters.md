---
title: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V4_PARAMETERS
description: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V4_PARAMETERS では、IPv4 のオフロードを開始する必要があるかどうかを示す OID_WDI_SET_ENCAPSULATION_OFFLOAD で使用される TLV です。
ms.assetid: DC474D05-BF41-48F4-90CC-96C3B7F41ED0
ms.date: 07/18/2017
keywords:
- WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V4_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f985e6e96744a971406f9e8c3cadd820708dee5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362808"
---
# <a name="wditlvsetencapsulationoffloadv4parameters"></a>WDI\_TLV\_設定\_カプセル化\_オフロード\_V4\_パラメーター


WDI\_TLV\_設定\_カプセル化\_オフロード\_V4\_パラメーターで使用される TLV [OID\_WDI\_設定\_カプセル化\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-encapsulation-offload)を IPv4 オフロードを開始する必要があるかどうかを示します。

## <a name="tlv-type"></a>TLV 型


0 xfd

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 型  | 説明                                                                                                                                             |
|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | IPv4 のオフロードを開始する必要があるかどうかを指定します。 NDIS にこの設定は\_オフロード\_設定\_ON を有効にして、NDIS に設定\_オフロード\_設定\_無効になっている場合はオフです。 |

 

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

## <a name="see-also"></a>関連項目


[**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)

 

 




