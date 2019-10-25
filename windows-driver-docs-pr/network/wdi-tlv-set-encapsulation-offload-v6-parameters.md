---
title: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS
description: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS は、IPv6 オフロードを開始する必要があるかどうかを示すために OID_WDI_SET_ENCAPSULATION_OFFLOAD によって使用される TLV です。
ms.assetid: 7036AFD0-197E-4A94-8580-A42889BE6798
ms.date: 07/18/2017
keywords:
- WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: c67b4357335b618be82db93f64f9ff903ac6baca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841726"
---
# <a name="wdi_tlv_set_encapsulation_offload_v6_parameters"></a>WDI\_TLV\_設定\_カプセル化\_オフロード\_V6\_パラメーター


WDI\_TLV\_SET\_のカプセル化\_オフロード\_V6\_パラメーターは、 [OID\_WDI\_設定\_カプセル化\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-encapsulation-offload)を使用して IPv6 オフロードが必要かどうかを示す TLV です。開始します。

## <a name="tlv-type"></a>TLV 型


0xFE

## <a name="length"></a>長さ


UINT8 のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに  | 説明                                                                                                                                             |
|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | IPv6 オフロードを開始する必要があるかどうかを指定します。 この値は、NDIS\_オフロード\_設定されている場合はオン\_オンになっている場合はオンになっています。また、無効になっている場合は、NDIS\_オフロード\_設定\_オフ |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

 

 




