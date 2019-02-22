---
title: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY
description: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY では、検出されたサービスのエントリを含む TLV です。
ms.assetid: B8D453FF-49CA-4106-97DA-008893760E92
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5f657e41339098fd4d7e0b0f7840ca4c4dda5725
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527589"
---
# <a name="wditlvp2pdiscoveredserviceentry"></a>WDI\_TLV\_P2P\_検出\_サービス\_エントリ


WDI\_TLV\_P2P\_検出\_サービス\_エントリが検出されたサービスのエントリを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x112

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                           | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                               |
|--------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_名**](wdi-tlv-p2p-service-name.md)               |                                |          | Utf-8、最大 255 バイトでは、サービスの名前。                                                                                                                       |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md) |                                | X        | サービスのサービス情報。                                                                                                                                  |
| [**WDI\_TLV\_P2P\_サービス\_状態**](wdi-tlv-p2p-service-status.md)           |                                |          | サービスのサービスの状態。                                                                                                                                        |
| [**WDI\_TLV\_P2P\_広告\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | サービス インスタンスを一意に識別する ID です。                                                                                                                      |
| [**WDI\_TLV\_P2P\_CONFIG\_メソッド**](wdi-tlv-p2p-config-methods.md)           |                                |          | 構成の方法で定義されている[ **WDI\_WPS\_構成\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/dn898198)します。 PinDisplay PinKeypad や WFDS は適用できます。 |

 

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

 

 




