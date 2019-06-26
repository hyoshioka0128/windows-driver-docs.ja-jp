---
title: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY では、アドバタイズされたサービスのエントリを含む TLV です。
ms.assetid: C9BBA5D4-EC51-4D03-B997-A95B3168E64F
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d12da79de0c8c091a28698906661acfd0b028702
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385710"
---
# <a name="wditlvp2padvertisedserviceentry"></a>WDI\_TLV\_P2P\_アドバタイズ\_サービス\_エントリ


WDI\_TLV\_P2P\_アドバタイズ\_サービス\_エントリがアドバタイズされたサービスのエントリを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0 xfc

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                           | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_名**](wdi-tlv-p2p-service-name.md)               |                                |          | Utf-8、最大 255 バイトでは、サービスの名前です。                                                                                                                          |
| [**WDI\_TLV\_P2P\_サービス\_名前\_ハッシュ**](wdi-tlv-p2p-service-name-hash.md)    |                                |          | サービス名のハッシュです。                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md) |                                | x        | このサービスのサービス情報。                                                                                                                                    |
| [**WDI\_TLV\_P2P\_サービス\_状態**](wdi-tlv-p2p-service-status.md)           |                                |          | このサービスのサービスの状態。                                                                                                                                          |
| [**WDI\_TLV\_P2P\_広告\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | サービス インスタンスを一意に識別する ID です。                                                                                                                     |
| [**WDI\_TLV\_P2P\_CONFIG\_メソッド**](wdi-tlv-p2p-config-methods.md)           |                                |          | 構成の方法で定義されている[ **WDI\_WPS\_構成\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_wps_configuration_method)します。 暗証番号 (pin) の表示、暗証番号 (pin) のキーパッドおよび WFDS は適用できます。 |

 

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

 

 




