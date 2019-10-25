---
title: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY は、ASP2 のアドバタイズされたサービスエントリを含む TLV です。
ms.assetid: CF7ED750-1987-4784-9E61-516EBBA22B9B
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f62ba25ea795025f3bdda4345e008e76da3c5823
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840326"
---
# <a name="wdi_tlv_p2p_asp2_advertised_service_entry"></a>WDI\_TLV\_P2P\_ASP2\_アドバタイズされる\_サービス\_エントリ


WDI\_TLV\_P2P\_ASP2\_アドバタイズされたサービス\_エントリは、ASP2 提供サービスエントリを含む TLV です。

この TLV は、Windows 10 バージョン1607、WDI version 1.0.21 で追加された  に**注意**してください。

 

## <a name="tlv-type"></a>TLV 型


0x12E

## <a name="length"></a>長さ


含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                           | 複数の TLV インスタンスを使用できます | オプション | 説明                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_型**](wdi-tlv-p2p-service-type.md)               |                                |          | サービスのサービスの種類 (UTF-8) (最大21バイト)。                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_サービス\_型\_HASH**](wdi-tlv-p2p-service-type-hash.md)    |                                |          | サービスの種類のハッシュ。                                                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_インスタンス\_名**](wdi-tlv-p2p-instance-name.md)             |                                |          | サービスのインスタンスの種類 (UTF-8)。最大63バイトです。                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_インスタンス\_名前\_ハッシュ**](wdi-tlv-p2p-instance-name-hash.md)  |                                |          | "インスタンス名, サービスの種類" のハッシュ。                                                                                                                                                                                                                                                   |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md) |                                | X        | サービスのサービス情報。                                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_サービス\_の状態**](wdi-tlv-p2p-service-status.md)           |                                |          | サービスのサービスの状態。                                                                                                                                                                                                                                                           |
| [**WDI\_TLV\_P2P\_提供情報\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | サービスインスタンスを一意に識別する ID。                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_CONFIG\_メソッド**](wdi-tlv-p2p-config-methods.md)           |                                |          | [**WDI\_WPS\_構成\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)で定義されている構成方法。 **WDI\_wps\_configuration\_メソッド\_表示**、 **WDI\_wps\_構成\_メソッド\_キーパッド**、および**WDI\_wps\_構成\_方法のみ @no既定では、\_既定値**が適用されます。 |

 

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

 

 




