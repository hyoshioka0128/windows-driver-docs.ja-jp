---
title: WDI_TLV_ASSOCIATION_RESULT
description: WDI_TLV_ASSOCIATION_RESULT では、アソシエーションの結果を含む TLV です。
ms.assetid: E0059A7A-0D20-403E-9A46-9633396A87C4
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESULT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d556abb4211f97a067c2013035cddbd46df70d9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376243"
---
# <a name="wditlvassociationresult"></a>WDI\_TLV\_アソシエーション\_結果


WDI\_TLV\_アソシエーション\_アソシエーションの結果を含む TLV になります。

## <a name="tlv-type"></a>TLV 型


0x35

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                       | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                 |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                                                   |                                |          | BSS の BSSID します。                                                                                                                                                                                       |
| [**WDI\_TLV\_アソシエーション\_結果\_パラメーター**](wdi-tlv-association-result-parameters.md) |                                |          | アソシエーション結果パラメーター。                                                                                                                                                                          |
| [**WDI\_TLV\_アソシエーション\_要求\_フレーム**](wdi-tlv-association-request-frame.md)         |                                | x        | 関連付けに使用されたアソシエーション要求。 これは、802.11 MAC ヘッダーには含まれません。                                                                                                         |
| [**WDI\_TLV\_アソシエーション\_応答\_フレーム**](wdi-tlv-association-response-frame.md)       |                                | x        | アソシエーションの応答を受信しました。 これは、802.11 MAC ヘッダーには含まれません。                                                                                                                    |
| [**WDI\_TLV\_AUTHENTICATION\_RESPONSE\_FRAME**](wdi-tlv-authentication-response-frame.md) |                                | x        | エラー コードを受信した認証の応答。 これは、802.11 MAC ヘッダーには含まれません。 だけことが含まれる認証交換中に、接続試行が失敗した場合。 |
| [**WDI\_TLV\_ビーコン\_プローブ\_応答**](wdi-tlv-beacon-probe-response.md)                 |                                | x        | 最新では、ビーコンまたはプローブ ポートで受信した応答フレーム。 これは、802.11 MAC ヘッダーには含まれません。                                                                                                |
| [**WDI\_TLV\_ETHERTYPE\_全て\_テーブル**](wdi-tlv-ethertype-encap-table.md)                 |                                | x        | アソシエーションの Ethertype カプセル化します。                                                                                                                                                           |
| [**WDI\_TLV\_PHY\_型\_一覧**](wdi-tlv-phy-type-list.md)                                 |                                | x        | BSS ネットワーク接続のパケットを送受信する 802.11 ステーションを使用する PHY 識別子の一覧。                                                                                          |

 

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

 

 




