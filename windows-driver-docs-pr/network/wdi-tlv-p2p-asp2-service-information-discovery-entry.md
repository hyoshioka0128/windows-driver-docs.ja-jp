---
title: WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY
description: WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY は、ASP2 サービス情報の検出エントリを含む TLV です。
ms.assetid: 67F1CDE2-8003-44D3-B338-FE7C5EA48C29
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b33c81a656e84895a10024b79a393cbac6d299ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550211"
---
# <a name="wditlvp2pasp2serviceinformationdiscoveryentry"></a>WDI\_TLV\_P2P\_ASP2\_サービス\_情報\_検出\_エントリ


WDI\_TLV\_P2P\_ASP2\_サービス\_情報\_検出\_エントリが ASP2 サービス情報の検出エントリを含む TLV します。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x12D

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                      | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                         |
|-------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_名**](wdi-tlv-p2p-service-name.md)                          |                                |          | 最大 21 バイト (utf-8)、サービスの名前です。                                                                        |
| [**WDI\_TLV\_P2P\_INSTANCE\_NAME**](wdi-tlv-p2p-instance-name.md)                        |                                |          | 最大 63 バイト (utf-8)、サービスのインスタンスの名前です。                                                               |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md)            |                                | X        | このサービスのサービス情報をダウンロードする ANQP クエリ要求に使用するサービスの情報を要求します。 |
| [**WDI\_TLV\_P2P\_サービス\_UPDATE\_インジケーター**](wdi-tlv-p2p-service-update-indicator.md) |                                | X        | ANQP クエリ要求に使用するサービスの更新のインジケーター。                                                     |
| [**WDI\_TLV\_P2P\_サービス\_トランザクション\_ID**](wdi-tlv-p2p-service-transaction-id.md)     |                                | X        | ANQP クエリ要求に使用するサービスのトランザクション ID。                                                       |

 

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

 

 




