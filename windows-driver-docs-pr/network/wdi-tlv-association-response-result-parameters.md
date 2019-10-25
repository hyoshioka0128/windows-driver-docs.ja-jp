---
title: WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS は、アソシエーション応答の結果パラメーターを含む TLV です。
ms.assetid: 8BF2C8B4-207E-479A-9903-3FCDEED5BA2C
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESPONSE_RESULT_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 875d7bb4f0677db391d146c8069e5b123a2f32fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842883"
---
# <a name="wdi_tlv_association_response_result_parameters"></a>WDI\_TLV\_アソシエーション\_応答\_結果\_パラメーター


WDI\_TLV\_アソシエーション\_応答\_結果\_パラメーターは、アソシエーション応答の結果パラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x76

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)"><strong>WDI_MAC_ADDRESS</strong></a></td>
<td>ピアアダプターの MAC アドレス。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>ピアステーションからの要求が再関連付け要求かどうかを示すビット値。
<p>有効な値は0と1です。 値1は、再関連付け要求であることを示します。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>ピアステーションからの応答が再関連付け応答であるかどうかを示すビット値。
<p>有効な値は0と1です。 値が1の場合は、再関連付けの応答であることを示します。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm" data-raw-source="[&lt;strong&gt;WDI_AUTH_ALGORITHM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)"><strong>WDI_AUTH_ALGORITHM</strong></a></td>
<td>アソシエーションの認証アルゴリズム。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)"><strong>WDI_CIPHER_ALGORITHM</strong></a></td>
<td>アソシエーションのユニキャスト暗号アルゴリズム。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)"><strong>WDI_CIPHER_ALGORITHM</strong></a></td>
<td>アソシエーションのマルチキャスト暗号アルゴリズム。</td>
</tr>
</tbody>
</table>

 

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

 

 




