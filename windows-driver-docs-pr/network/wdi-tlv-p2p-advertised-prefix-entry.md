---
title: WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY
description: WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY を含む Wi-Fi Direct TLV は、プレフィックスのエントリを提供します。
ms.assetid: 484A7784-EDD5-46F0-91E0-060D23ADC0BD
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ADVERTISED_PREFIX_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a4018c0eeb561d6963a43c14f37fe40252e8617e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383167"
---
# <a name="wditlvp2padvertisedprefixentry"></a>WDI\_TLV\_P2P\_アドバタイズ\_プレフィックス\_エントリ


WDI\_TLV\_P2P\_アドバタイズ\_プレフィックス\_エントリを含む Wi-Fi Direct TLV は、プレフィックスのエントリを提供します。

## <a name="tlv-type"></a>TLV 型


0x110

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                      |
|-----------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_名**](wdi-tlv-p2p-service-name.md)            |                                |          | 255 バイトの最大サイズ: utf-8 では、サービスの名前です。 |
| [**WDI\_TLV\_P2P\_サービス\_名前\_ハッシュ**](wdi-tlv-p2p-service-name-hash.md) |                                |          | サービス名のハッシュです。                                            |

 

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

 

 




