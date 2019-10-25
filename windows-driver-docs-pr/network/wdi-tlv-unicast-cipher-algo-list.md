---
title: WDI_TLV_UNICAST_CIPHER_ALGO_LIST
description: WDI_TLV_UNICAST_CIPHER_ALGO_LIST は、ユニキャスト暗号アルゴリズムの一覧を含む TLV です。
ms.assetid: 67FAEE8A-1CD6-4430-92C1-84E9F43BEF63
ms.date: 07/18/2017
keywords:
- WDI_TLV_UNICAST_CIPHER_ALGO_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 9278599b641c82bb7707e7d2749ff14f9d9b77f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841718"
---
# <a name="wdi_tlv_unicast_cipher_algo_list"></a>WDI\_TLV\_ユニキャスト\_暗号\_ALGO\_LIST


WDI\_TLV\_ユニキャスト\_暗号\_ALGO\_LIST は、ユニキャスト暗号アルゴリズムの一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x3E

## <a name="length"></a>長さ


[**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)構造体の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                            | 説明                            |
|-----------------------------------------------------------------|----------------------------------------|
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)\[\] | ユニキャスト暗号アルゴリズムの配列。 |

 

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

 

 




