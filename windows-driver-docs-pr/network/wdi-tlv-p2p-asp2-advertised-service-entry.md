---
title: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY は、ASP2 提供サービス エントリを含む TLV です。
ms.assetid: CF7ED750-1987-4784-9E61-516EBBA22B9B
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b62a8ec597ebb665e6c6b411f554786c33a8df47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379734"
---
# <a name="wditlvp2pasp2advertisedserviceentry"></a>WDI\_TLV\_P2P\_ASP2\_アドバタイズ\_サービス\_エントリ


WDI\_TLV\_P2P\_ASP2\_アドバタイズ\_サービス\_エントリが ASP2 提供サービス エントリを含む TLV します。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x12E

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                           | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_型**](wdi-tlv-p2p-service-type.md)               |                                |          | 最大 21 バイト (utf-8)、サービスのサービスの種類。                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_サービス\_型\_ハッシュ**](wdi-tlv-p2p-service-type-hash.md)    |                                |          | サービスの種類のハッシュです。                                                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_INSTANCE\_NAME**](wdi-tlv-p2p-instance-name.md)             |                                |          | 最大 63 バイトに (utf-8)、サービスの種類をインスタンスします。                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_INSTANCE\_NAME\_HASH**](wdi-tlv-p2p-instance-name-hash.md)  |                                |          | 「インスタンス名、サービスの種類」のハッシュです。                                                                                                                                                                                                                                                   |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md) |                                | x        | サービスのサービス情報。                                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_サービス\_状態**](wdi-tlv-p2p-service-status.md)           |                                |          | サービスのサービスの状態。                                                                                                                                                                                                                                                           |
| [**WDI\_TLV\_P2P\_広告\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | サービス インスタンスを一意に識別する ID です。                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_CONFIG\_メソッド**](wdi-tlv-p2p-config-methods.md)           |                                |          | 構成の方法で定義されている[ **WDI\_WPS\_構成\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_wps_configuration_method)します。 のみ**WDI\_WPS\_構成\_メソッド\_表示**、 **WDI\_WPS\_構成\_メソッド\_キーパッド**、および**WDI\_WPS\_構成\_メソッド\_WFDS\_既定**適用されます。 |

 

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

 

 




