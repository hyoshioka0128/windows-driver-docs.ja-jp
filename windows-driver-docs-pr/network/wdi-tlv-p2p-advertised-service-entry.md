---
title: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY では、アドバタイズされたサービスのエントリを含む TLV です。
ms.assetid: C9BBA5D4-EC51-4D03-B997-A95B3168E64F
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c4f317c9659282abaad0ac7833cf6b388dcdc8c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347268"
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
| [**WDI\_TLV\_P2P\_CONFIG\_メソッド**](wdi-tlv-p2p-config-methods.md)           |                                |          | 構成の方法で定義されている[ **WDI\_WPS\_構成\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/dn898198)します。 暗証番号 (pin) の表示、暗証番号 (pin) のキーパッドおよび WFDS は適用できます。 |

 

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

 

 




