---
title: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY は、提供されたサービスエントリを含む TLV です。
ms.assetid: C9BBA5D4-EC51-4D03-B997-A95B3168E64F
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: fd6238b890ca9dc37843e3bcdce661e672919066
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842629"
---
# <a name="wdi_tlv_p2p_advertised_service_entry"></a>WDI\_TLV\_P2P\_\_提供されるサービスの\_エントリ


WDI\_TLV\_P2P\_通知される\_サービス\_エントリは、提供されたサービスエントリを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xFC

## <a name="length"></a>長さ


含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                           | 複数の TLV インスタンスを使用できます | オプション | 説明                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_名**](wdi-tlv-p2p-service-name.md)               |                                |          | サービスの名前。 UTF-8 では、最大255バイトです。                                                                                                                          |
| [**WDI\_TLV\_P2P\_サービス\_名前\_ハッシュ**](wdi-tlv-p2p-service-name-hash.md)    |                                |          | サービス名のハッシュ。                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md) |                                | X        | このサービスのサービス情報。                                                                                                                                    |
| [**WDI\_TLV\_P2P\_サービス\_の状態**](wdi-tlv-p2p-service-status.md)           |                                |          | このサービスのサービスの状態。                                                                                                                                          |
| [**WDI\_TLV\_P2P\_提供情報\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | サービスインスタンスを一意に識別する ID。                                                                                                                     |
| [**WDI\_TLV\_P2P\_CONFIG\_メソッド**](wdi-tlv-p2p-config-methods.md)           |                                |          | [**WDI\_WPS\_構成\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)で定義されている構成方法。 ピンの表示、ピンパッド、およびその他の場合にのみ適用できます。 |

 

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

 

 




