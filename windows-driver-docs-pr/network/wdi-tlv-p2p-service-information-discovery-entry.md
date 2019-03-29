---
title: WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY
description: WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY では、サービス情報の検出のエントリを含む TLV です。
ms.assetid: 344A1E76-26E0-4816-8BA5-24F4784B48A1
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f37c5576c785f7680d0fd8e3892baade1464d774
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580469"
---
# <a name="wditlvp2pserviceinformationdiscoveryentry"></a>WDI\_TLV\_P2P\_サービス\_情報\_検出\_エントリ


WDI\_TLV\_P2P\_サービス\_情報\_検出\_エントリは、サービス情報の検出のエントリを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x117

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 型                                                                                      | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                         |
|-------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_名**](wdi-tlv-p2p-service-name.md)                          |                                |          | 最大 255 バイト (utf-8)、サービスの名前です。                                                                       |
| [**WDI\_TLV\_P2P\_サービス\_名前\_ハッシュ**](wdi-tlv-p2p-service-name-hash.md)               |                                |          | サービス名のハッシュです。                                                                                               |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md)            |                                | x        | このサービスのサービス情報をダウンロードする ANQP クエリ要求に使用するサービスの情報を要求します。 |
| [**WDI\_TLV\_P2P\_サービス\_UPDATE\_インジケーター**](wdi-tlv-p2p-service-update-indicator.md) |                                | x        | ANQP クエリ要求に使用するサービスの更新のインジケーター。                                                     |
| [**WDI\_TLV\_P2P\_サービス\_トランザクション\_ID**](wdi-tlv-p2p-service-transaction-id.md)     |                                | x        | ANQP クエリ要求に使用するサービスのトランザクション ID。                                                       |

 

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

 

 




