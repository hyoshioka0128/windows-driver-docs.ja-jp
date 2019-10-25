---
title: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY
description: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY は、検出されたサービスエントリを含む TLV です。
ms.assetid: B8D453FF-49CA-4106-97DA-008893760E92
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 1723107597ab9127e073e4685357126be1103fd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840447"
---
# <a name="wdi_tlv_p2p_discovered_service_entry"></a>WDI\_TLV\_P2P\_検出された\_サービス\_エントリ


WDI\_TLV\_P2P\_検出された\_サービス\_エントリは、検出されたサービスエントリを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x112

## <a name="length"></a>Length


含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| 種類                                                                           | 複数の TLV インスタンスを使用できます | 省略可能 | 説明                                                                                                                                                               |
|--------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_名**](wdi-tlv-p2p-service-name.md)               |                                |          | サービスの名前。 UTF-8 では、最大255バイトです。                                                                                                                       |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md) |                                | ○        | サービスのサービス情報。                                                                                                                                  |
| [**WDI\_TLV\_P2P\_サービス\_の状態**](wdi-tlv-p2p-service-status.md)           |                                |          | サービスのサービスの状態。                                                                                                                                        |
| [**WDI\_TLV\_P2P\_提供情報\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | サービスインスタンスを一意に識別する ID。                                                                                                                      |
| [**WDI\_TLV\_P2P\_CONFIG\_メソッド**](wdi-tlv-p2p-config-methods.md)           |                                |          | [**WDI\_WPS\_configuration\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)で定義されている構成方法。 有効なのは、PinDisplay、Pindisplay、およびを適用した場合のみです。 |

 

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最低限のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小サーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




